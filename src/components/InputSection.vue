<template>
  <div class="input-section">
    <h2>Abstände Festlegen</h2>
    <div v-for="(circle, index) in formattedCircles" :key="index" class="circle-input">
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
  computed: {
    formattedCircles() {
      return this.circles.map((circle) => ({
        x: Number(circle.x).toFixed(2),
        y: Number(circle.y).toFixed(2),
      }));
    },
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

.input-section h2 {
  font-size: 28px;
  margin-bottom: 20px;
}

.circle-input {
  margin-bottom: 20px;
  padding: 15px;
  background-color: #ffffff;
  border-radius: 15px;
  box-sizing: border-box;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
}

.input-group {
  margin-bottom: 10px;
}

.input-group label {
  display: block;
  margin-bottom: 5px;
  font-size: 14px;
  color: #1c1c1e;
}

.input-group input {
  width: 100%;
  padding: 12px;
  border-radius: 10px;
  border: 1px solid #d1d1d6;
  font-size: 16px;
  background-color: #f2f2f7;
  box-sizing: border-box;
}

.input-group input:focus {
  border-color: #007aff;
  background-color: #ffffff;
}

.input-section button {
  padding: 12px 20px;
  background-color: #34c759;
  color: #fff;
  border: none;
  border-radius: 12px;
  cursor: pointer;
  font-size: 16px;
  transition: background-color 0.3s;
}

.input-section button:hover {
  background-color: #28a745;
}
</style>
