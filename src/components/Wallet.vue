<template>
  <div class="py-6 px-6 lg:px-8">
    <h3 class="mb-4 text-xl font-medium text-gray-900 dark:text-white">
      Top-up wallet:
    </h3>
    <form @submit.prevent="topUpWallet" class="space-y-6" action="#">
      <div>
        <label
          for="amt"
          class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
          >Enter amount:</label
        >
        <input
          v-model="edit_info.amount"
          type="number"
          name="amt"
          id="amt"
          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-600 dark:border-gray-500 dark:placeholder-gray-400 dark:text-white"
          placeholder=""
          required
        />
      </div>
      <button
        type="submit"
        class="w-full text-white bg-sky-500 hover:bg-sky-600 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-sky-500 dark:focus:ring-sky-600"
      >
        Top-up
      </button>
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Wallet",
  data() {
    return {
      edit_info: {
        userId: localStorage.logged,
        amount: "",
      },
    };
  },
  methods: {
    async topUpWallet() {
      const resp = await axios.post(
        "http://localhost:8080/user/wallet",
        this.edit_info
      );
      window.location.reload();
    },
  },
};
</script>
