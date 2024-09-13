<template>
    <div class="progress-bar" :style="{ width: progress + '%' }"></div>
  </template>
  
  <script>
  export default {
    name: "ProgressBar",
    data() {
      return {
        progress: 0
      };
    },
    mounted() {
      this.startProgress();
    },
    methods: {
      startProgress() {
        let interval = setInterval(() => {
          if (this.progress >= 100) {
            clearInterval(interval);
          } else {
            this.progress += 1;
          }
        }, 100);
      }
    }
  };
  </script>
  
  <style scoped>
  .progress-bar {
    height: 5px;
    background-color: green;
    transition: width 0.1s;
  }
  </style>
  