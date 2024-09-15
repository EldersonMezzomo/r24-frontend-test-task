<template>
  <div class="material-selection">
    <h2>Materialauswahl</h2>
    <div class="materials">
      <div
        v-for="material in materials"
        :key="material"
        :class="['material-item', { selected: selectedMaterial === material }]"
        @click="selectMaterial(material)"
      >
        {{ material }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MaterialSelection',
  data() {
    return {
      materials: ['Holz', 'Metall', 'Kunststoff', 'Glas', 'Keramik'],
    };
  },
  props: {
    selectedMaterial: String,
  },
  methods: {
    selectMaterial(material) {
      this.$emit('select-material', material);
    },
  },
};
</script>

<style scoped>
.material-selection {
  margin-bottom: 30px;
}

.material-selection h2 {
  font-size: 28px;
  margin-bottom: 20px;
}

.materials {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
}

.material-item {
  padding: 12px 20px;
  background-color: #f2f2f7;
  border-radius: 12px;
  cursor: pointer;
  font-size: 16px;
  color: #1c1c1e;
  transition: background-color 0.3s, transform 0.2s;
}

.material-item:hover {
  background-color: #e5e5ea;
}

.material-item.selected {
  background-color: #007aff;
  color: #fff;
}

.material-item:active {
  transform: scale(0.98);
}
</style>
