<template>
    <div class="background" :class="backgroundClass"></div>
  </template>
  
  <script>
  export default {
    name: "BackgroundTransition",
    data() {
      return {
        backgroundClass: 'white-background'
      };
    },
    mounted() {
      setTimeout(() => {
        this.backgroundClass = 'black-background';
      }, 5000); // 5 segundos para transição
    }
  };
  </script>
  
  <style scoped>
  .background {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    transition: background-color 1s;
  }
  .white-background {
    background-color: white;
  }
  .black-background {
    background-color: black;
  }
  </style>
  