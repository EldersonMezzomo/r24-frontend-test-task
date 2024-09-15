<template>
  <div
    class="circle"
    :style="{ left: position.x + 'px', top: position.y + 'px' }"
    @mousedown="startDrag"
  ></div>
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
  background-color: #007aff;
  border-radius: 50%;
  transform: translate(-50%, -50%);
  cursor: grab;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  transition: transform 0.2s;
}

.circle:active {
  transform: translate(-50%, -50%) scale(0.95);
}
</style>
