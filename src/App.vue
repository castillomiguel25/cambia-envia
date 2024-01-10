<template>
  <main>
    <Px-header :links="links" />
    <div class="margin-body">
      <router-view class="container sm:px-20 py-20 flex justify-center" />
    </div>
  </main>
</template>

<script>
import PxHeader from "@/components/PxHeader";

export default {
  data() {
    return {
      links: [
        {
          title: "BTC",
          to: { name: "coin-detail", params: { id: "bitcoin" } },
        },
        {
          title: "ETH",
          to: { name: "coin-detail", params: { id: "ethereum" } },
        },
        {
          title: "XRP",
          to: { name: "coin-detail", params: { id: "xrp" } },
        },
      ],
    };
  },

  name: "App",
  components: {
    PxHeader,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 0px;
  overflow-x: hidden;
}

.margin-body {
  margin-left: 20px;
  margin-right: 20px;
}
body {
  overflow-x: hidden;
}
</style>
