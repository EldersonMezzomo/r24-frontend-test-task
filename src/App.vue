<template>
  <div class="app-container">
    <div class="content-wrapper">
      <div class="main-content">
        <!-- Seção da Imagem -->
        <div class="image-section">
          <ImageSection
            ref="imageSection"
            :circles="circles"
            @start-drag="startDrag"
          />
        </div>

        <!-- Seção de Customizações -->
        <div class="customization-section">
          <!-- Título Rotacionado -->
          <div class="rotated-title">
            <span>Anpassungen</span>
          </div>
          <!-- Bloco de Inputs e Seleção de Material -->
          <div class="customization-content">
            <InputSection
              :circles="circles"
              @add-circle="addCircle"
              @update-circle="updateCircle"
            />
            <MaterialSelection
              :selectedMaterial="selectedMaterial"
              @select-material="selectMaterial"
            />
            <button class="submit-button" @click="submitData">Senden</button>
          </div>
        </div>
      </div>

      <!-- Seção de Dados Submetidos -->
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
        }
      }
    },
    stopDrag() {
      this.isDragging = false;
      document.removeEventListener('mousemove', this.onDrag);
      document.removeEventListener('mouseup', this.stopDrag);
    },
    updateCircle(index, x, y) {
      const rect = this.$refs.imageSection.$refs.imageContainer.getBoundingClientRect();
      x = Math.max(0, Math.min(x, rect.width));
      y = Math.max(0, Math.min(y, rect.height));

      if (!this.isColliding(x, y, index)) {
        this.circles[index] = { x, y };
      }
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
          xPixels: circle.x.toFixed(2),
          yPixels: circle.y.toFixed(2),
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
body {
  margin: 0;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell,
    'Open Sans', 'Helvetica Neue', sans-serif;
  background-color: #ffffff;
  color: #1c1c1e;
}

h1,
h2,
h3,
h4,
h5,
h6 {
  font-weight: normal;
}

a {
  color: #007aff;
  text-decoration: none;
}

button {
  font-family: inherit;
}

.app-container {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

.content-wrapper {
  max-width: 960px;
  margin: 0 auto;
  padding: 0 10px; /* Garante uma distância mínima de 10px nas laterais */
  flex: 1;
  width: 100%;
  box-sizing: border-box;
}

.main-content {
  display: flex;
  flex: 1;
}

.image-section {
  flex: 1;
  display: flex;
  justify-content: center;
  align-items: center;
}

.customization-section {
  flex: 1;
  position: relative;
  background-color: #f9f9f9;
  display: flex;
}

.rotated-title {
  position: absolute;
  top: 20px;
  left: -50px;
  writing-mode: vertical-rl;
  text-orientation: mixed;
  transform: rotate(180deg);
  font-size: 24px;
  color: #7f7f7f;
}

.customization-content {
  margin: auto;
  width: 80%;
  max-width: 400px;
}

.submit-button {
  padding: 15px 30px;
  background-color: #007aff;
  color: #fff;
  border: none;
  border-radius: 12px;
  cursor: pointer;
  font-size: 16px;
  transition: background-color 0.3s;
}

.submit-button:hover {
  background-color: #005fcb;
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

@media (max-width: 768px) {
  .main-content {
    flex-direction: column;
  }

  .customization-section {
    position: static;
    width: 100%;
  }

  .rotated-title {
    position: static;
    transform: none;
    writing-mode: horizontal-tb;
    text-align: center;
    margin-bottom: 20px;
  }

  .customization-content {
    width: 100%;
    max-width: none;
  }

  .image-section,
  .customization-section {
    flex: none;
  }

  /* Adicionar ajuste para a imagem */
  .image-section {
    padding: 20px 0;
    max-width: 100%;
  }

  .image-section img {
    max-width: 100%;
    height: auto;
  }
 }
</style>
