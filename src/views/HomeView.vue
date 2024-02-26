<template>
  <v-container fluid class="background-container">
    <img src="/assets/images/PesquisaCEP.png" alt="Logo" style="height: 150px">
      <BackgroundImage />
      <v-sheet class="d-flex align-center justify-center flex-wrap text-center mx-auto px-4" elevation="4" height="250" rounded max-width="800" width="100%">
          <div>
              <h2 class="text-h4 font-weight-black text-green">Buscando um CEP?</h2>
  
              <div class="text-h5 font-weight-medium mb-2">
                  Vou te ajudar nessa! 
              </div>
  
              <p class="text-body-2 mb-4">
                  Clique não botão a baixo e busque seu CEP
              </p>
              <v-btn @click="redirectToSearchCep">Pesquisar CEP</v-btn>
          </div>
      </v-sheet>
  </v-container>
  </template>
  
  <script>
  import BackgroundImage from '@/components/BackgroundImage.vue';
  
  export default {
      name: 'HomeView',
      components: {
        BackgroundImage,
      },
      methods: {
        redirectToSearchCep() {
          this.$router.push('/SearchCep');
      },
  },
  }
  </script>
  <style>
  .background-container {
    position: relative;
    z-index: 0;
  }
</style>