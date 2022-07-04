<template>
  <div>
    <div class="border-b border-lgprtwo mb-4 p-3" v-for="(p, index) in cart" :key="p.id">
      <p class="mb-2">{{ p.title }}</p>
      <p>Price: <span class="text-prpl font-semibold">{{ p.price }}</span></p>
      <button @click="deleteFromCartLocal(index)" class="my-2 p-3 text-prpl hover:bg-white rounded-lg transition">
        Delete from cart
      </button>
    </div>
  </div>
</template>

<script>
import { ref } from '@vue/reactivity';
import { deleteFromCart } from '../utils/cart'
export default {
  setup() {
    let cart = ref(JSON.parse(sessionStorage.getItem('cart')));
    const deleteFromCartLocal = (index) => {
      cart.value.splice(index,1)
      deleteFromCart(index)
    }
    return {
      cart,
      deleteFromCart,
      deleteFromCartLocal
    }
  },
};
</script>
