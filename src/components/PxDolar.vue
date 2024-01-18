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
            <td class="border px-6 py-4">
              {{ dollarData.price.toFixed(2) }} bs
            </td>
          </tr>
          <tr
            class="border-b border-gray-200 hover:bg-gray-100 hover:bg-orange-100"
            v-if="dollarDataBcv"
          >
            <td class="border px-6 py-4">{{ "Dolar BCV" }}</td>
            <td class="border px-6 py-4">{{ dollarDataBcv.last_update }}</td>
            <td class="border px-6 py-4">
              {{ dollarDataBcv.price.toFixed(2) }} bs
            </td>
          </tr>
        </tbody>
      </table>
      <div
        v-if="dollarData"
        class="flex-col items-center justify-center mt-10 font-bold px-10"
      >
        <div class="mb-3">
          <p>Calcular Precio Dolar Paralelo</p>
        </div>

        <div class="flex-col items-center">
          <button
            @click="selectedInput = 'usd'"
            class="ml-2 mr-2 p-2 border border-gray-300 rounded"
          >
            Dólares ($)
          </button>
          <button
            @click="selectedInput = 'bs'"
            class="ml-2 mr-2 p-2 border border-gray-300 rounded"
          >
            Bolívares (BS)
          </button>

          <div class="flex-col mt-3">
            <input
              v-if="selectedInput === 'usd'"
              v-model="userInputOne"
              type="number"
              class="ml-2 mr-2 p-2 border border-gray-300 rounded"
              placeholder="cantidad en $"
            />

            <input
              v-if="selectedInput === 'bs'"
              v-model="userInputOneBs"
              type="number"
              class="ml-2 mr-2 p-2 border border-gray-300 rounded"
              placeholder="cantidad en Bolívares"
            />
          </div>

          <p class="mt-3" v-if="selectedInput === 'usd'">
            {{ (userInputOne * dollarData.price).toFixed(2) }} BS
          </p>

          <p class="mt-3" v-if="selectedInput === 'bs'">
            {{ (userInputOneBs / dollarData.price).toFixed(2) }} $
          </p>
        </div>
      </div>










      <div
        v-if="dollarDataBcv"
        class="flex-col items-center justify-center mt-10 font-bold px-10"
      >
        <div class="mb-3">
          <p>Calcular Precio Dolar BCV</p>
        </div>
        <div class="flex-col items-center">
          <button
            @click="selectedInputTwo = 'usd'"
            class="ml-2 mr-2 p-2 border border-gray-300 rounded"
          >
            Dólares ($)
          </button>
          <button
            @click="selectedInputTwo = 'bs'"
            class="ml-2 mr-2 p-2 border border-gray-300 rounded"
          >
            Bolívares (BS)
          </button>

          <div class="flex-col mt-3">
            <input
              v-if="selectedInputTwo === 'usd'"
              v-model="userInput"
              type="number"
              class="ml-2 mr-2 p-2 border border-gray-300 rounded"
              placeholder="cantidad en $"
            />
            <input
              v-if="selectedInputTwo === 'bs'"
              v-model="userInputOneBcv"
              type="number"
              class="ml-2 mr-2 p-2 border border-gray-300 rounded"
              placeholder="cantidad en Bolívares"
            />
          </div>
        </div>

        <p class="mt-3" v-if="selectedInputTwo === 'usd'">
          {{ (userInput * dollarDataBcv.price).toFixed(2) }} BS
        </p>
        <p class="mt-3" v-if="selectedInputTwo === 'bs'">
          {{ (userInputOneBcv / dollarDataBcv.price).toFixed(2) }} $
        </p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      selectedInput: "",
      selectedInputTwo: "",
      dollarData: null,
      dollarDataBcv: null,
      userInputOne: 0,
      userInputOneBs: 0,
      userInput: 0,
      userInputOneBcv: 0,
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
