<template>
  <div class="py-6 px-6 lg:px-8">
    <h2 class="mb-4 text-xl font-medium text-gray-900 dark:text-white">
      Success!
    </h2>
    <div>
      <h3>Your order has been placed.</h3>
    </div>
    <br /><br />
    <button
      @click="goToMain"
      type="button"
      class="w-full text-white bg-sky-500 hover:bg-sky-600 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-sky-500 dark:focus:ring-sky-600"
    >
      Home Page
    </button>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "CheckoutPopUp",
  data() {
    return {};
  },
  methods: {
    goToMain() {
      this.$router.push("/main");
    },
  },
};
</script>
