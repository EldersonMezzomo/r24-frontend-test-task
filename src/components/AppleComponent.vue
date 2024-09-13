<template>
    <div class="apple" :class="appleClass"></div>
  </template>
  
  <script>
  export default {
    name: "AppleComponent",
    data() {
      return {
        appleClass: 'red-apple'
      };
    },
    methods: {
      changeToSilver() {
        this.appleClass = 'silver-apple';
      }
    }
  };
  </script>
  
  <style scoped>
  .apple {
    width: 100px;
    height: 100px;
    border-radius: 50%;
    transition: background-color 1s;
  }
  .red-apple {
    background-color: red;
  }
  .silver-apple {
    background-color: silver;
  }
  </style>
  