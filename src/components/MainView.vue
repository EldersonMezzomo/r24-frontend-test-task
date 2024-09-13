<template>
  <div>
    <!-- Barra de Progresso -->
    <ProgressBar />
    
    <!-- Pac-Man se movendo -->
    <PacMan />
    
    <!-- Transição de fundo de branco para preto -->
    <BackgroundTransition />
    
    <!-- Componente da maçã -->
    <AppleComponent ref="appleComponent" />
  </div>
</template>

<script>
import ProgressBar from './ProgressBar.vue';   // Importando o componente da barra de progresso
import PacMan from './PacMan.vue';             // Importando o componente PacMan
import BackgroundTransition from './BackgroundTransition.vue'; // Importando o componente da transição de fundo
import AppleComponent from './AppleComponent.vue';  // Importando o componente Apple

export default {
  name: "MainView",
  components: {
    ProgressBar,
    PacMan,
    BackgroundTransition,
    AppleComponent
  },
  mounted() {
    // Depois de 7 segundos, a maçã muda de cor
    setTimeout(() => {
      this.$refs.appleComponent.changeToSilver();  // Acessando o método do componente AppleComponent via referência
    }, 7000); // Maçã mudará de cor após 7 segundos
  }
};
</script>

<style scoped>
/* Aqui você pode adicionar o estilo para a MainView, caso necessário */
</style>
