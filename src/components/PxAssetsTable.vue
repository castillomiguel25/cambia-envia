<template>
  <div class="flex justify-center items-center md:px-20 sm:flex-col w-full">
    <div>
      <table class="min-w-full bg-white shadow-md rounded">
        <thead class="bg-purple-400 text-white">
          <tr class="bg-purple-300 border-b-2 border-purple-400">
            <th></th>
            <th
              class="px-6 py-4 text-left font-bold  delete-mobile"
              :class="{ up: this.sortOrder === 1, down: this.sortOrder === -1 }"
            >
              <span class="underline cursor-pointer" @click="changeSortOrder"
                >Ranking</span
              >
            </th>
            <th>Nombre</th>
            <th>Precio</th>

            <th>Variación 24hs</th>
            <td class="hidden sm:block">
              <input
                class="bg-purple-100 focus:outline-none border-b text-black border-purple-400 py-2 px-4 block w-full appearance-none leading-normal"
                id="filter"
                placeholder="Buscar..."
                type="text"
                v-model="filter"
              />
            </td>
          </tr>
        </thead>
        <tbody>
          <tr
            v-for="a in filteredAssets"
            :key="a.id"
            class="border-b border-gray-200 hover:bg-gray-100 hover:bg-orange-100"
          >
            <td>
              <img
                class="mx-6 w-12 h-12"
                :src="`https://static.coincap.io/assets/icons/${a.symbol.toLowerCase()}@2x.png`"
                :alt="a.name"
              />
            </td>
            <td class="delete-mobile">
              <b># {{ a.rank }} </b>
            </td>

            <td>
              <router-link
                class="hover:underline text-green-600 "
                :to="{ name: 'coin-detail', params: { id: a.id } }"
                >{{ a.name }}</router-link
              >
              <small class="ml-1 text-gray-500">{{ a.symbol }} </small>
            </td>

            <td>${{ new Intl.NumberFormat("es-CO").format(a.priceUsd) }}</td>

            <td
              :class="
                a.changePercent24Hr.includes('-')
                  ? 'text-red-600'
                  : 'text-green-600'
              "
            >
              {{ Math.round(a.changePercent24Hr * 100) / 100 }}
            </td>
            <td class="hidden sm:block">
              <px-button @click="goToCoin(a.id)">
                <span> Detalle </span>
              </px-button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import PxButton from "@/components/PxButton";

export default {
  name: "PxAssetsTable",

  components: { PxButton },

  data() {
    return {
      filter: "",
      sortOrder: 1,
    };
  },

  props: {
    assets: {
      type: Array,
      default: () => [],
    },
  },

  computed: {
    filteredAssets() {
      const altOrder = this.sortOrder === 1 ? -1 : 1;

      return this.assets
        .filter(
          (a) =>
            a.symbol.toLowerCase().includes(this.filter.toLowerCase()) ||
            a.name.toLowerCase().includes(this.filter.toLowerCase())
        )
        .sort((a, b) => {
          if (parseInt(a.rank) > parseInt(b.rank)) {
            return this.sortOrder;
          }

          return altOrder;
        });
    },
  },

  methods: {
    goToCoin(id) {
      this.$router.push({ name: "coin-detail", params: { id } });
    },

    changeSortOrder() {
      this.sortOrder = this.sortOrder === 1 ? -1 : 1;
    },
  },
};
</script>

<style scoped>
table {
  width: 100%;
  table-layout: fixed;
}

/* Esto ocultará la barra de desplazamiento horizontal */

.up::before {
  content: "🔼";
}

.down::before {
  content: "🔻";
}

td {
  padding: 20px 0px;
  font-size: 0.8rem;
  text-align: center;
}

@media (min-width: 640px) {
  td,
  th {
    padding: 20px;
    font-size: 1rem;
  }

  th {
    padding: 12px;
  }
}

@media only screen and (max-width: 600px) {
  .delete-mobile {
    display: none;
  }
}
</style>
