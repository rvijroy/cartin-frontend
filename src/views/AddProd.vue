<template>
  <Disclosure as="nav" class="bg-zinc-50" v-slot="{ open }">
    <div class="mx-auto max-w-7xl px-2 sm:px-6 lg:px-8">
      <div class="relative flex h-16 items-center justify-between">
        <div class="absolute inset-y-0 left-0 flex items-center sm:hidden">
          <!-- Mobile menu button-->
          <DisclosureButton
            class="inline-flex items-center justify-center rounded-md p-2 text-gray-400 hover:bg-gray-700 hover:text-white focus:outline-none focus:ring-2 focus:ring-inset focus:ring-white"
          >
            <span class="sr-only">Open main menu</span>
            <Bars3Icon v-if="!open" class="block h-6 w-6" aria-hidden="true" />
            <XMarkIcon v-else class="block h-6 w-6" aria-hidden="true" />
          </DisclosureButton>
        </div>
        <div
          class="flex flex-1 items-center justify-center sm:items-stretch sm:justify-start"
        >
          <div class="flex flex-shrink-0 items-center">
            <router-link to="/mainadm"
              ><img
                class="img max-h-8"
                src="../assets/shop.png"
                alt=""
                srcset=""
            /></router-link>
          </div>
          <div class="sm:ml-6 sm:block">
            <div class="flex space-x-4">
              <h2 class="font-sansserif text-lg text-white pt-1 ml-3 mr-7">
                Add Product
              </h2>
              <router-link
                to="/customerlist"
                :class="[
                  active
                    ? 'bg-sky-500 text-white'
                    : 'text-black hover:bg-sky-500 hover:text-white',
                  'px-3 py-2 rounded-md text-sm font-medium',
                ]"
                >Reports</router-link
              >
              <router-link
                to="/manadmlist"
                :class="[
                  active
                    ? 'bg-sky-500 text-white'
                    : 'text-black hover:bg-sky-500 hover:text-white',
                  'px-3 py-2 rounded-md text-sm font-medium',
                ]"
                >Managers</router-link
              >
              <router-link
                to="/prodbydate"
                :class="[
                  active
                    ? 'bg-sky-500 text-white'
                    : 'text-black hover:bg-sky-500 hover:text-white',
                  'px-3 py-2 rounded-md text-sm font-medium',
                ]"
                >Product By Date</router-link
              >
            </div>
          </div>
        </div>

        <div
          class="absolute inset-y-0 right-0 flex items-center pr-2 sm:static sm:inset-auto sm:ml-6 sm:pr-0"
        >
          <!-- Profile dropdown -->
          <Menu as="div" class="relative ml-3 z-50">
            <div>
              <MenuButton
                class="flex rounded-full bg-zinc-50 text-sm focus:outline-none focus:ring-2 focus:ring-white focus:ring-offset-2 focus:ring-offset-gray-800"
              >
                <span class="sr-only">Open user menu</span>
                <div
                  class="overflow-hidden relative w-10 h-10 bg-gray-100 rounded-full dark:bg-gray-600"
                >
                  <svg
                    class="absolute -left-1 w-12 h-12 text-gray-400"
                    fill="currentColor"
                    viewBox="0 0 20 20"
                    xmlns="http://www.w3.org/2000/svg"
                  >
                    <path
                      fill-rule="evenodd"
                      d="M10 9a3 3 0 100-6 3 3 0 000 6zm-7 9a7 7 0 1114 0H3z"
                      clip-rule="evenodd"
                    ></path>
                  </svg>
                </div>
              </MenuButton>
            </div>
            <transition
              enter-active-class="transition ease-out duration-100"
              enter-from-class="transform opacity-0 scale-95"
              enter-to-class="transform opacity-100 scale-100"
              leave-active-class="transition ease-in duration-75"
              leave-from-class="transform opacity-100 scale-100"
              leave-to-class="transform opacity-0 scale-95"
            >
              <MenuItems
                class="absolute right-0 z-10 mt-2 w-48 origin-top-right rounded-md bg-white py-1 shadow-lg ring-1 ring-black ring-opacity-5 focus:outline-none"
              >
                <MenuItem v-slot="{ active }">
                  <a
                    href="/account"
                    :class="[
                      active ? 'bg-gray-100' : '',
                      'block px-4 py-2 text-sm text-gray-700',
                    ]"
                    >Your Profile</a
                  >
                </MenuItem>
                <MenuItem v-slot="{ active }">
                  <a
                    href="/rstpass"
                    :class="[
                      active ? 'bg-gray-100' : '',
                      'block px-4 py-2 text-sm text-gray-700',
                    ]"
                    >Change Password</a
                  >
                </MenuItem>
                <MenuItem v-slot="{ active }">
                  <a
                    @click="logoutUser"
                    :class="[
                      active ? 'bg-gray-100' : '',
                      'block px-4 py-2 text-sm text-gray-700',
                    ]"
                    >Sign out</a
                  >
                </MenuItem>
              </MenuItems>
            </transition>
          </Menu>
        </div>
      </div>
    </div>
  </Disclosure>
  <div class="bg-white">
    <div class="pt-6">
      <div
        class="mx-auto mt-6 max-w-2xl sm:px-6 lg:grid lg:max-w-7xl lg:grid-cols-2 lg:gap-x-8 lg:px-8"
      >
        <div
          class="aspect-w-3 aspect-h-4 hidden overflow-hidden rounded-lg lg:block"
        >
          <div class="flex items-center justify-center w-full pt-9">
            <label
              for="dropzone-file"
              class="flex flex-col items-center justify-center pt-2 w-full h-64 border-2 border-gray-300 border-dashed rounded-lg cursor-pointer bg-gray-50 dark:hover:bg-bray-800 dark:bg-gray-700 hover:bg-gray-100 dark:border-gray-600 dark:hover:border-gray-500 dark:hover:bg-gray-600"
            >
              <div class="flex flex-col items-center justify-center pt-5 pb-6">
                <img
                  v-if="visible"
                  :src="product.image"
                  class="h-full w-full object-cover object-center"
                />
                <!-- <input
                  id="dropzone-file"
                  type="file"
                  accept="image/jpeg"
                  class="hidden"
                  @change="uploadImage"
                /> -->
              </div>
            </label>
          </div>
        </div>

        <div>
          <form
            @submit.prevent="addProduct"
            class="mt-8 space-y-6"
            action="#"
            method="POST"
          >
            <input type="hidden" name="remember" value="true" />
            <div class="-space-y-px rounded-md shadow-sm">
              <h1 class="pt-0">Add Product:</h1>
              <div>
                <label
                  for="name"
                  class="block text-sm font-medium text-gray-700 pt-4 pb-3"
                  >Name</label
                >
                <input
                  v-model="product.name"
                  id="name"
                  name="name"
                  type="text"
                  autocomplete=""
                  required=""
                  class="relative block w-full appearance-none rounded-none rounded-t-md border border-gray-300 px-3 py-2 text-gray-900 placeholder-gray-500 focus:z-10 focus:border-sky-500 focus:outline-none focus:ring-sky-500 sm:text-sm"
                  placeholder=""
                />
              </div>
              <div>
                <label
                  for="desc"
                  class="block text-sm font-medium text-gray-700 pt-4 pb-3"
                  >Description</label
                >
                <input
                  v-model="product.description"
                  id="desc"
                  name="desc"
                  type="text"
                  autocomplete=""
                  required=""
                  class="relative block w-full appearance-none rounded-none rounded-t-md border border-gray-300 px-3 py-2 text-gray-900 placeholder-gray-500 focus:z-10 focus:border-sky-500 focus:outline-none focus:ring-sky-500 sm:text-sm"
                  placeholder=""
                />
              </div>
              <div>
                <label
                  for="price"
                  class="block text-sm font-medium text-gray-700 pt-4 pb-3"
                  >Price</label
                >
                <input
                  v-model="product.price"
                  id="price"
                  name="price"
                  type="number"
                  min="0"
                  autocomplete=""
                  required=""
                  class="relative block w-full appearance-none rounded-none rounded-t-md border border-gray-300 px-3 py-2 text-gray-900 placeholder-gray-500 focus:z-10 focus:border-sky-500 focus:outline-none focus:ring-sky-500 sm:text-sm"
                  placeholder=""
                />
              </div>
              <div>
                <label
                  for="image"
                  class="block text-sm font-medium text-gray-700 pt-4 pb-3"
                  >Image URL</label
                >
                <input
                  v-model="product.image"
                  id="image"
                  name="image"
                  type="text"
                  autocomplete=""
                  required=""
                  class="relative block w-full appearance-none rounded-none rounded-t-md border border-gray-300 px-3 py-2 text-gray-900 placeholder-gray-500 focus:z-10 focus:border-sky-500 focus:outline-none focus:ring-sky-500 sm:text-sm"
                  placeholder=""
                />
              </div>
              <div>
                <label
                  for="q"
                  class="block text-sm font-medium text-gray-700 pt-4 pb-3"
                  >Quantity</label
                >
                <input
                  v-model="product.quantity"
                  id="q"
                  name="q"
                  type="number"
                  min="0"
                  autocomplete=""
                  required=""
                  class="relative block w-full appearance-none rounded-none rounded-t-md border border-gray-300 px-3 py-2 text-gray-900 placeholder-gray-500 focus:z-10 focus:border-sky-500 focus:outline-none focus:ring-sky-500 sm:text-sm"
                  placeholder=""
                />
              </div>
              <div>
                <label
                  for="q"
                  class="block text-sm font-medium text-gray-700 pt-4 pb-3"
                  >Category</label
                >
                <select
                  v-model="product.category"
                  class="form-select appearance-none block w-full px-3 py-1.5 text-base font-normal text-gray-700 bg-white bg-clip-padding bg-no-repeat border border-solid border-gray-300 rounded transition ease-in-out m-0 focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none"
                  aria-label="Default select example"
                >
                  <option value="0">Home Appliance</option>
                  <option value="1">Stationery</option>
                  <option value="2">Groceries</option>
                  <option value="3">Food</option>
                  <option value="4">Miscellanious</option>
                </select>
              </div>
              <div>
                <label
                  for="address"
                  class="block text-sm font-medium text-gray-700 pt-4 pb-3"
                  >Delivery time (days)</label
                >
                <input
                  v-model="product.deliveryTime"
                  id="del"
                  min="0"
                  name="del"
                  type="number"
                  autocomplete=""
                  required=""
                  class="relative block w-full appearance-none rounded-none rounded-t-md border border-gray-300 px-3 py-2 text-gray-900 placeholder-gray-500 focus:z-10 focus:border-sky-500 focus:outline-none focus:ring-sky-500 sm:text-sm"
                  placeholder=""
                />
              </div>
              <div>
                <label
                  for="offer"
                  class="block text-sm font-medium text-gray-700 pt-4 pb-3"
                  >Offer (% off)</label
                >
                <input
                  v-model="product.offer"
                  id="offer"
                  name="offer"
                  type="number"
                  min="0"
                  max="100"
                  autocomplete=""
                  required=""
                  class="relative block w-full appearance-none rounded-none rounded-t-md border border-gray-300 px-3 py-2 text-gray-900 placeholder-gray-500 focus:z-10 focus:border-sky-500 focus:outline-none focus:ring-sky-500 sm:text-sm"
                  placeholder=""
                />
              </div>
            </div>
            <button
              type="submit"
              class="group relative flex w-full justify-center rounded-md border border-transparent bg-sky-500 py-2 px-4 text-sm font-medium text-white hover:bg-sky-600 focus:outline-none focus:ring-2 focus:ring-sky-500 focus:ring-offset-2"
            >
              Add Product
            </button>
          </form>
        </div>
      </div>
    </div>
  </div>
  <div
    v-if="show"
    class="overflow-x-hidden overflow-y-auto fixed inset-0 z-50 outline-none focus:outline-none justify-center items-center flex"
  >
    <div class="relative w-full max-w-md h-full md:h-auto">
      <div class="relative bg-white rounded-lg shadow dark:bg-gray-700">
        <button
          @click="showSuccess()"
          type="button"
          class="absolute top-3 right-2.5 text-gray-400 bg-transparent hover:bg-gray-200 hover:text-gray-900 rounded-lg text-sm p-1.5 ml-auto inline-flex items-center dark:hover:bg-zinc-50 dark:hover:text-white"
          data-modal-toggle="wallet-modal"
        >
          <svg
            aria-hidden="true"
            class="w-5 h-5"
            fill="currentColor"
            viewBox="0 0 20 20"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              fill-rule="evenodd"
              d="M4.293 4.293a1 1 0 011.414 0L10 8.586l4.293-4.293a1 1 0 111.414 1.414L11.414 10l4.293 4.293a1 1 0 01-1.414 1.414L10 11.414l-4.293 4.293a1 1 0 01-1.414-1.414L8.586 10 4.293 5.707a1 1 0 010-1.414z"
              clip-rule="evenodd"
            ></path>
          </svg>
          <span class="sr-only">Close modal</span>
        </button>
        <AddedProduct mode="added to"></AddedProduct>
      </div>
    </div>
  </div>
  <div v-if="show" class="opacity-25 fixed inset-0 z-40 bg-black"></div>
  <Footer></Footer>
</template>

<script>
import {
  Disclosure,
  DisclosureButton,
  DisclosurePanel,
  Menu,
  MenuButton,
  MenuItem,
  MenuItems,
} from "@headlessui/vue";
import { Bars3Icon, BellIcon, XMarkIcon } from "@heroicons/vue/24/outline";
import AddedProduct from "../components/AddedProduct.vue";
import Footer from "../components/Footer.vue";
export default {
  name: "AddProd_new",
  components: {
    AddedProduct,
    Footer,
    Disclosure,
    DisclosureButton,
    DisclosurePanel,
    Menu,
    MenuButton,
    MenuItem,
    MenuItems,
    Bars3Icon,
    BellIcon,
    XMarkIcon,
  },
  data() {
    return {
      product: {
        name: "",
        description: "",
        price: 0,
        quantity: 0,
        category: "",
        deliveryTime: 0,
        offer: 0,
        image: "",
      },
      visible: false,
      previewImage: null,
      show: false,
    };
  },
  methods: {
    // uploadImage(e) {
    //   const image = e.target.files[0];
    //   const reader = new FileReader();
    //   reader.readAsDataURL(image);
    //   reader.onload = (e) => {
    //     this.previewImage = e.target.result;
    //     this.product.image = this.previewImage.slice(23);
    //     this.visible = true;
    //   };
    // },
    async logoutUser() {
      await axios.post("http://localhost:8080/user/logout", {
        userId: localStorage.logged,
      });
      localStorage.removeItem("logged");
      this.$router.push("/");
    },
    addProduct() {
      axios
        .post("http://localhost:8080/admin/addProduct", {
          senderId: localStorage.logged,
          product: this.product,
        })
        // .then((resp) => this.saveImage(resp.data))
        .then(this.showSuccess());
    },
    showSuccess() {
      this.show = !this.show;
    },
  },
};
</script>
