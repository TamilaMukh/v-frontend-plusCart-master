<template>
  <div class="w-full px-3 lg:px-0 lg:w-4/5 mx-auto mt-20">
    <div class="lg:flex lg:items-center mb-14">
    <h1 class="font-semibold my-3 mr-20">Product</h1>
    <p class="hover:text-prpl transition"><router-link to="/products">Back</router-link></p>
    </div>
    <div v-if="fetching" class="loader w-full container mx-auto mt-40"></div>
    <div v-else-if="error">
      Oh no... {{ error }}
    </div>
    <div v-else>
      <div v-if="data">
        <div class="w-4/5 my-6 flex">
        <div class="bg-neutral-100 rounded-lg p-10 border-b border-lghtprpl transition"><img :src="'http://38.242.229.113:8055/assets/' + data.products_by_id.image.id" alt=""></div>
          <div class="w-1/3 mx-20 bg-neutral-100 rounded-lg p-3 border-b border-lghtprpl">
            <p class="font-semibold mb-6 border-b border-b-neutral-300">{{ data.products_by_id.title }}</p>
            <p class="text-prpl">Characteristic:</p>
            <p class="my-2 border-b">Price: {{ data.products_by_id.price }}</p>
            <p class="my-2 border-b">{{ data.products_by_id.description }}</p>
            <p class="my-2 border-b">text</p>
            <p class="my-2 border-b">text</p>
            <p class="my-2 border-b">text</p>
          </div>
          <!-- <div class="text-center">
            <p class="bg-lgprtwo rounded-lg p-3 h-18 mb-5 cursor-pointer hover:text-prpl transition">Add to cart</p>
            <p class="bg-lgprtwo rounded-lg p-3 h-12 mt-5 cursor-pointer hover:text-prpl transition">Buy</p>
          </div> -->
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { useRoute } from "vue-router";
import { useQuery, gql } from "@urql/vue";
export default {
  name: "Product",
  setup() {
    const route = useRoute();
    const getProductQuery = gql`
      query ($id: ID!) {
        products_by_id(id: $id) {
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
    const getProduct = useQuery({ query: getProductQuery, variables: { id: route.params.id } });
    return {
      fetching: getProduct.fetching,
      data: getProduct.data,
      error: getProduct.error,
    };
  },
};
</script>

<style scoped></style>
