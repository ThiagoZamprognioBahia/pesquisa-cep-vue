<template>
    <div class="background-image"></div>
  </template>
  
  <script>
  export default {
    name: 'BackgroundImage'
  }
  </script>
  
  <style scoped>
  .background-image {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-image: url('/public/assets/images/background.jpg'); /* Caminho para sua imagem */
    background-size: cover;
    background-position: center center; 
    z-index: -1
  }
  </style>