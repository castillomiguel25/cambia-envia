<!-- vistas componentes de vue -->
<template>
  <div class="flex flex-col items-center justify-center">
    <ring-loader
      :loading="isloading"
      :color="'#68d391'"
      :size="'300px'"
    ></ring-loader>
    <div class="mb-5">
        <px-dolar  v-if="!isloading" />
    </div>
  </div>
</template>

<script>
import api from "@/api";
import RingLoader from "vue-spinner/src/RingLoader.vue";
import PxDolar from "@/components/PxDolar.vue";

export default {
  name: "Home",

  components: { RingLoader, PxDolar },

  data() {
    return {
      isloading: false,
      assets: [],
    };
  },

  created() {
    this.isloading = true;

    api
      .getAssets()
      .then((assets) => (this.assets = assets))
      .finally(() => (this.isloading = false));
  },
};
</script>
<style scoped></style>
