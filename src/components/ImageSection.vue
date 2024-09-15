<template>
  <div class="image-section">
    <div class="image-container" ref="imageContainer">
      <img src="@/assets/atari-console.png" alt="Atari Console" />
      <DraggableCircle
        v-for="(circle, index) in circles"
        :key="index"
        :position="circle"
        :index="index"
        @start-drag="startDrag"
      />
    </div>
  </div>
</template>

<script>
import DraggableCircle from './DraggableCircle.vue';

export default {
  name: 'ImageSection',
  components: { DraggableCircle },
  props: {
    circles: Array,
  },
  methods: {
    startDrag(index) {
      this.$emit('start-drag', index);
    },
  },
};
</script>

<style scoped>
.image-section {
  margin-bottom: 30px;
}

.image-container {
  position: relative;
  display: inline-block;
  cursor: pointer;
}

.image-container img {
  max-width: 100%;
  border-radius: 20px;
}
</style>