<template>
    <div class="flex justify-center">
      <div v-if="dollarData" class="max-w-sm rounded overflow-hidden shadow-lg mx-4">
        <div class="px-6 py-4 bg-purple-300">
          <div class="font-bold text-xl mb-2">Paralero</div>
          <p class="text-white font-bold">Última actualización: {{ dollarData.last_update }}</p>
          <p class="text-white font-bold">Precio Actual: {{ dollarData.price }}</p>
        </div>
      </div>
  
      <div v-if="dollarDataBcv" class="max-w-sm rounded overflow-hidden shadow-lg mx-4">
        <div class="px-6 py-4 bg-purple-300">
          <div class="font-bold text-xl mb-2">BCV</div>
          <p class="text-white font-bold">Última actualización: {{ dollarDataBcv.last_update }}</p>
          <p class="text-white font-bold">Precio Actual: {{ dollarDataBcv.price }}</p>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        dollarData: null,
        dollarDataBcv: null
      };
    },
    mounted() {
      this.fetchDollarData();
      this.fetchDollarDataBcv();
    },
    methods: {
      async fetchDollarData() {
        try {
          const response = await fetch('https://pydolarvenezuela-api.vercel.app/api/v1/dollar/unit/enparalelovzla');
          const data = await response.json();
          this.dollarData = data;
        } catch (error) {
          console.error('Error al obtener los datos del dólar en Venezuela', error);
        }
      },
      async fetchDollarDataBcv() {
        try {
          const response = await fetch('https://pydolarvenezuela-api.vercel.app/api/v1/dollar/unit/bcv');
          const data = await response.json();
          this.dollarDataBcv = data;
        } catch (error) {
          console.error('Error al obtener los datos del dólar en Venezuela', error);
        }
      }
    }
  };
  </script>
  