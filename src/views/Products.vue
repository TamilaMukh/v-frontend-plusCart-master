<template>
  <div class="w-full px-3 lg:px-0 lg:w-4/5 mx-auto mt-20">
    <div class="lg:flex lg:items-center lg:justify-between">
      <h1 class="font-semibold my-6 lg:my-3 lg:mr-20">Products</h1>
    <p class="lg:mr-20 text-prpl font-semibold">{{ searchString }}</p>
    <div class="w-full my-6 mx-auto lg:flex items-center">
      <input
        class="lg:w-1/3 p-1 font-light border border-gray-400 rounded-lg mr-3 hover:border hover:border-prpl focus:outline-lghtprpl"
        type="text"
        placeholder="Search..."
        v-model="searchString"
      />
      <i class="fas fa-search relative right-10"></i>
      <div class="flex items-center">
        <p class="mr-3">min</p> <input
        class="p-1 font-light border border-gray-400 rounded-lg mr-3 hover:border hover:border-prpl focus:outline-lghtprpl"
        type="text"
        placeholder="Min"
        v-model.number="min"
      />
      </div>
      <div class="flex items-center">
        <p class="mr-3">max</p> <input
        class="p-1 font-light border border-gray-400 rounded-lg mr-3 hover:border hover:border-prpl focus:outline-lghtprpl"
        type="text"
        placeholder="Max"
        v-model.number="max"
      />
      </div>
    </div>
    </div>
    <div v-if="fetching" class="loader w-full container mx-auto mt-40"></div>
    <div v-else-if="error">Oh no... {{ error }}</div>
    <div v-else>
      <div v-if="data" class="lg:flex lg:flex-wrap">
        <div v-for="p in data.products" :key="p.id" class="w-full lg:w-1/5 bg-neutral-100 border rounded-lg m-3 p-3 hover:bg-black/10 transition" @click="move(p.id)">
        <img class="w-4/5 rounded-lg mx-auto" :src="'http://38.242.229.113:8055/assets/' + p.image.id" alt="">
        <div class="text-base text-center mt-6 items-center justify-between">
          <p class="font-medium mb-2">{{ p.title }}</p>
          <p>
            Price:
            <span class="text-prpl font-semibold">{{ p.price }}</span>
          </p>
          <button @click="addToCart(p)" class="mt-3 p-3 text-prpl hover:bg-neutral-100 rounded-lg transition">Add to cart</button>
        </div>
        </div>
        <button class="h-12 w-40 m-3 p-3 border bg-neutral-100 rounded-lg hover:bg-black/10 hover:text-prpl transition" @click="limit += 10">
          Show more...
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import { useQuery, gql } from "@urql/vue";
import { addToCart } from '@/utils/cart';
import { useRouter } from "vue-router";
import { ref } from "@vue/reactivity";
export default {
name: "Products",
  // data() {
  //   return {
  //   }
  // },
  setup() {
    const limit = ref(10);
    const router = useRouter();
    const searchString = ref(null);
    const min = ref(0);
    const max = ref(10000000);
    const getProductsQuery = gql`
      query ($search: String, $min: Float, $max: Float, $limit: Int! = 10) {
        products(
          search: $search
          filter: {
            _and: [{ price: { _gte: $min } }, { price: { _lte: $max } }]
          }
          limit: $limit
        ) {
          id
          title
          price
          description
          image {
            id
          }
        }
      }
    `;
    const move = (id) => router.push("/products/" + id);
    const getProducts = useQuery({
      query: getProductsQuery,
      variables: { search: searchString, min, max, variables: { limit } },
    });
    return {
      fetching: getProducts.fetching,
      data: getProducts.data,
      error: getProducts.error,
      move,
      searchString,
      min,
      max,
      limit,
      addToCart
    };
  },
};
</script>

<style scoped></style>
