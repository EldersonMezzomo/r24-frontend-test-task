<template>
  <div class="input-section">
    <h2>Abstände Festlegen</h2>
    <div v-for="(circle, index) in circles" :key="index" class="circle-input">
      <h3>Kreis {{ index + 1 }}</h3>
      <div class="input-group">
        <label>Abstand X:</label>
        <input
          type="number"
          :value="circle.x"
          @input="updateX($event, index)"
        />
      </div>
      <div class="input-group">
        <label>Abstand Y:</label>
        <input
          type="number"
          :value="circle.y"
          @input="updateY($event, index)"
        />
      </div>
    </div>
    <button @click="addCircle">Kreis Hinzufügen</button>
  </div>
</template>

<script>
export default {
  name: 'InputSection',
  props: {
    circles: Array,
  },
  methods: {
    addCircle() {
      this.$emit('add-circle');
    },
    updateX(event, index) {
      const x = Number(event.target.value);
      this.$emit('update-circle', index, x, this.circles[index].y);
    },
    updateY(event, index) {
      const y = Number(event.target.value);
      this.$emit('update-circle', index, this.circles[index].x, y);
    },
  },
};
</script>

<style scoped>
.input-section {
  margin-bottom: 30px;
}

.circle-input {
  margin-bottom: 20px;
}

.input-group {
  margin-bottom: 10px;
}

.input-group label {
  display: block;
  margin-bottom: 5px;
}

.input-group input {
  width: 100%;
  padding: 8px;
  border-radius: 8px;
  border: 1px solid #ccc;
}

.input-section button {
  padding: 10px 20px;
  background-color: #007aff;
  color: #fff;
  border: none;
  border-radius: 10px;
  cursor: pointer;
}
</style>
