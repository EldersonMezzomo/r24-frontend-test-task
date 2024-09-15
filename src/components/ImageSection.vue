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
  background-color: #ffffff;
  display: flex;
  justify-content: center;
  align-items: center;
}

.image-container {
  position: relative;
  max-width: 100%;
  width: 100%;
  height: auto;
}

.image-container img {
  display: block;
  width: 100%;
  height: auto;
  max-width: 600px; /* Limita a largura máxima da imagem */
  border-radius: 20px;
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
}
</style>
