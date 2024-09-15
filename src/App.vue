<template>
  <div class="app-container">
    <InputSection ref="inputSection" :circles="circles" @add-circle="addCircle" @update-circle="updateCircle" />
    <ImageSection ref="imageSection" :circles="circles" @start-drag="startDrag" />
    <MaterialSelection :selectedMaterial="selectedMaterial" @select-material="selectMaterial" />
    <button class="submit-button" @click="submitData">Senden</button>

    <div v-if="submittedData.length > 0" class="submitted-data">
      <h2>Gesendete Daten</h2>
      <ul>
        <li v-for="(data, index) in submittedData" :key="index">
          <strong>Einsendung {{ index + 1 }}:</strong>
          <ul>
            <li>Material: {{ data.selectedMaterial }}</li>
            <li>Kreise:</li>
            <ul>
              <li v-for="(circle, cIndex) in data.circles" :key="cIndex">
                Kreis {{ cIndex + 1 }} - xPixels: {{ circle.xPixels }}, yPixels: {{ circle.yPixels }}, xPercent: {{
                  circle.xPercent }}, yPercent: {{ circle.yPercent }}
              </li>
            </ul>
          </ul>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import ImageSection from './components/ImageSection.vue';
import InputSection from './components/InputSection.vue';
import MaterialSelection from './components/MaterialSelection.vue';

export default {
  name: 'App',
  components: {
    ImageSection,
    InputSection,
    MaterialSelection,
  },
  data() {
    return {
      circles: [],
      isDragging: false,
      dragIndex: null,
      selectedMaterial: null,
      submittedData: [],
    };
  },
  methods: {
    addCircle() {
      if (this.circles.length < 5) {
        const rect = this.$refs.imageSection.$refs.imageContainer.getBoundingClientRect();
        const x = rect.width / 2;
        const y = rect.height / 2;
        if (!this.isColliding(x, y)) {
          this.circles.push({ x, y });
        } else {
          alert('Die Kreise dürfen sich nicht überschneiden.');
        }
      } else {
        alert('Maximale Anzahl von Kreisen erreicht.');
      }
    },
    startDrag(index) {
      this.dragIndex = index;
      this.isDragging = true;
      document.addEventListener('mousemove', this.onDrag);
      document.addEventListener('mouseup', this.stopDrag);
    },
    onDrag(event) {
      if (this.isDragging) {
        const rect = this.$refs.imageSection.$refs.imageContainer.getBoundingClientRect();
        let x = event.clientX - rect.left;
        let y = event.clientY - rect.top;

        x = Math.max(0, Math.min(x, rect.width));
        y = Math.max(0, Math.min(y, rect.height));

        if (!this.isColliding(x, y, this.dragIndex)) {
          this.circles[this.dragIndex] = { x, y };
          // Não precisamos mais chamar updateCircle no componente filho
        }
      }
    },
    updateCircle(index, x, y) {
      const rect = this.$refs.imageSection.$refs.imageContainer.getBoundingClientRect();
      x = Math.max(0, Math.min(x, rect.width));
      y = Math.max(0, Math.min(y, rect.height));

      if (!this.isColliding(x, y, index)) {
        this.circles[index] = { x, y };
      }
    },
    stopDrag() {
      this.isDragging = false;
      document.removeEventListener('mousemove', this.onDrag);
      document.removeEventListener('mouseup', this.stopDrag);
    },
    isColliding(x, y, excludeIndex = null) {
      const radius = 20;
      for (let i = 0; i < this.circles.length; i++) {
        if (i === excludeIndex) continue;
        const circle = this.circles[i];
        const dx = circle.x - x;
        const dy = circle.y - y;
        const distance = Math.sqrt(dx * dx + dy * dy);
        if (distance < radius * 2) {
          return true;
        }
      }
      return false;
    },
    selectMaterial(material) {
      this.selectedMaterial = material;
    },
    submitData() {
      const rect = this.$refs.imageSection.$refs.imageContainer.getBoundingClientRect();
      const imageWidth = rect.width;
      const imageHeight = rect.height;
      const outputData = {
        circles: this.circles.map((circle) => ({
          xPixels: circle.x,
          yPixels: circle.y,
          xPercent: ((circle.x / imageWidth) * 100).toFixed(2) + '%',
          yPercent: ((circle.y / imageHeight) * 100).toFixed(2) + '%',
        })),
        selectedMaterial: this.selectedMaterial,
      };
      this.submittedData.push(outputData);
      if (this.submittedData.length > 5) {
        this.submittedData.shift();
      }
      console.log(outputData);
    },
  },
};
</script>

<style>
.app-container {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell,
    'Open Sans', 'Helvetica Neue', sans-serif;
  padding: 20px;
}

.submit-button {
  padding: 15px 30px;
  background-color: #34c759;
  color: #fff;
  border: none;
  border-radius: 15px;
  cursor: pointer;
  font-size: 16px;
}

.submitted-data {
  margin-top: 30px;
}

.submitted-data h2 {
  margin-bottom: 15px;
}

.submitted-data ul {
  list-style-type: none;
  padding: 0;
}

.submitted-data li {
  margin-bottom: 10px;
}
</style>