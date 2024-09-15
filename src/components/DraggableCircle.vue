<template>
  <div class="circle" :style="{ left: position.x + 'px', top: position.y + 'px' }" @mousedown="startDrag"></div>
</template>

<script>
export default {
  name: 'DraggableCircle',
  props: {
    position: Object,
    index: Number,
  },
  methods: {
    startDrag() {
      this.$emit('start-drag', this.index);
    },
  },
};
</script>

<style scoped>
.circle {
  position: absolute;
  width: 40px;
  height: 40px;
  background-color: rgba(0, 122, 255, 0.8);
  border-radius: 50%;
  transform: translate(-50%, -50%);
  cursor: grab;
}
</style>