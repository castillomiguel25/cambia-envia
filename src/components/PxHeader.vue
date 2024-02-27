<template>
  <header class="shadow w-screen">
    <nav>
      <nav
        class="flex items-center justify-between flex-wrap bg-purple-800 p-10"
      >
        <div class="flex items-center flex-shrink-0 text-white mr-6">
          <router-link
            to="/"
            class="font-semibold text-teal-200 text-xl tracking-tight"
            >Cambia tu Dolar</router-link
          >
        </div>
      </nav>
    </nav>
  </header>
</template>

<script>
// import PxIcon from "@/components/PxIcon";

export default {
  name: "PxHeader",
  components: {
    // PxIcon,
  },

  props: {
    links: {
      type: Array,
      default: () => [],
    },
  },
};
</script>
