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

.materials {
  display: flex;
  flex-wrap: wrap;
}

.material-item {
  padding: 10px 20px;
  margin: 5px;
  background-color: #f2f2f2;
  border-radius: 15px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.material-item.selected {
  background-color: #007aff;
  color: #fff;
}
</style>