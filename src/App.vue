<template>
  <main>
    <Calculadora/>
  </main>
</template>

<script>
import Calculadora from './components/Calculadora/Calculadora.vue'

export default {
  name: 'App',
  components: {
    Calculadora
  }
}
</script>

<style scoped>
  @font-face {
      font-family: 'DigitalFont';
      src: url('@/assets/fonts/DS-DIGIB.TTF') format('truetype');
  }
  main {
    display: flex;
    justify-content: center;
    align-items: center;
    background-image: linear-gradient(45deg, rgb(52, 52, 52), rgb(255, 255, 255));
    height: 100vh;
    width: 80vw;
  }
</style>
