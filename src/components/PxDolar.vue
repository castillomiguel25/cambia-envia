<template>
  <div class="flex justify-center sm:flex-col px-20">
    <div>
      <table class="min-w-full bg-white shadow-md rounded">
        <thead class="bg-purple-400 text-white">
          <tr>
            <th class="px-6 py-4 text-left font-bold">Nombre</th>
            <th class="px-6 py-4 text-left font-bold">Última actualización</th>
            <th class="px-6 py-4 text-left font-bold">Precio Actual</th>
          </tr>
        </thead>
        <tbody>
          <tr
            class="border-b border-gray-200 hover:bg-gray-100 hover:bg-orange-100"
            v-if="dollarData"
          >
            <td class="border px-6 py-4">{{ "Dolar Paralero" }}</td>
            <td class="border px-6 py-4">{{ dollarData.last_update }}</td>
            <td class="border px-6 py-4">{{ dollarData.price }} bs</td>
          </tr>
          <tr
            class="border-b border-gray-200 hover:bg-gray-100 hover:bg-orange-100"
            v-if="dollarDataBcv"
          >
            <td class="border px-6 py-4">{{ "Dolar BCV" }}</td>
            <td class="border px-6 py-4">{{ dollarDataBcv.last_update }}</td>
            <td class="border px-6 py-4">{{ dollarDataBcv.price }} bs</td>
          </tr>
        </tbody>
      </table>
      <div class="mt-5">
        <p>Calcular Precio Dolar Paralelo</p>
      </div>
      <div
        v-if="dollarData"
        class="flex items-center justify-center mt-10 font-bold px-10"
      >
        <div class="flex-col items-center">
          <input
            v-model="userInputOne"
            type="number"
            class="ml-2 mr-2 p-2 border border-gray-300 rounded"
            placeholder="cantidad en $"
          />
          <p class="mt-3">{{ (userInputOne * dollarData.price).toFixed(3) }} BS</p>
        </div>
      </div>
      <div class="mt-5">
        <p>Calcular Precio Dolar BCV</p>
      </div>
      <div
        v-if="dollarDataBcv"
        class="flex items-center justify-center mt-10 font-bold px-10"
      >
        <div class="flex-col items-center">
          <input
            v-model="userInput"
            type="number"
            class="ml-2 mr-2 p-2 border border-gray-300 rounded"
            placeholder="cantidad en $"
          />
          <p class="mt-3">{{ (userInput * dollarDataBcv.price).toFixed(3) }} BS</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      dollarData: null,
      dollarDataBcv: null,
      userInputOne: 1,
      userInput: 1,
    };
  },
  mounted() {
    this.fetchDollarData();
    this.fetchDollarDataBcv();
  },
  methods: {
    async fetchDollarData() {
      try {
        const response = await fetch(
          "https://pydolarvenezuela-api.vercel.app/api/v1/dollar/unit/enparalelovzla"
        );
        const data = await response.json();
        this.dollarData = data;
      } catch (error) {
        console.error(
          "Error al obtener los datos del dólar en Venezuela",
          error
        );
      }
    },
    async fetchDollarDataBcv() {
      try {
        const response = await fetch(
          "https://pydolarvenezuela-api.vercel.app/api/v1/dollar/unit/bcv"
        );
        const data = await response.json();
        this.dollarDataBcv = data;
      } catch (error) {
        console.error(
          "Error al obtener los datos del dólar en Venezuela",
          error
        );
      }
    },
  },
};
</script>
