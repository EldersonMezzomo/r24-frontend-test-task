<template>
    <div class="pacman"></div>
  </template>
  
  <script>
  export default {
    name: "PacMan"
  };
  </script>
  
  <style scoped>
  .pacman {
    width: 100px;
    height: 100px;
    background-color: yellow;
    border-radius: 50%;
    position: absolute;
    top: 50%;
    left: 0;
    transform: translateY(-50%);
    animation: pacman-mouth 0.5s infinite, pacman-move 5s linear forwards;
  }
  
  @keyframes pacman-mouth {
    0%, 100% {
      clip-path: polygon(50% 50%, 0% 100%, 100% 100%);
    }
    50% {
      clip-path: polygon(50% 50%, 0% 80%, 100% 80%);
    }
  }
  
  @keyframes pacman-move {
    0% {
      left: 0;
    }
    100% {
      left: 50%;
      transform: translate(-50%, -50%);
    }
  }
  </style>
  