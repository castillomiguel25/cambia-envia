<template>
  <button
    @click="buttonClick"
    class="bg-transparent hover:bg-purple-700 text-purple-300 font-semibold hover:text-white py-2 px-2 border border-purple-500 hover:border-transparent rounded"
  >
    <p v-show="!isLoading">
      <slot></slot>
    </p>
  </button>
</template>

<script>
export default {
  name: "PxButton",

  props: {
    isLoading: {
      type: Boolean,
      default: false,
    },
  },

  methods: {
    buttonClick() {
      this.$emit("click");
    },
  },
};
</script>
