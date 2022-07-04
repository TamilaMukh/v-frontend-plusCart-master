<template>
    <div class="bg-white stiky top-0 left-0 right-0">
    <div class="w-1/2 lg:w-full bg-lghtgr">
      <div class="w-11/12 mx-auto p-5 items-center justify-between flex">
        <p class="font-semibold mx-2 text-prpl hover:text-lghtprpl transition"><router-link class="shopname" to="/">ma<span>Ғ</span>azin</router-link></p>
        <div class="w-1/4 h-1 bg-prpl rounded-xl"></div>
        <!-- <p class="hover:text-prpl transition"><router-link to="/">Home</router-link></p> -->
        <button @click="changeT()" class="flex items-center py-2 px-4 mx-2 bg-white hover:text-prpl transition rounded-lg">
          <p class="mx-1">Almaty</p><i class="fas fa-chevron-down text-xs ml-2"></i>
        </button>
        <div v-if="showTown === 1" class="frstDrop w-trn p-2 bg-neutral-100 text-center rounded-lg">
          <p class="mx-1 p-2 cursor-pointer hover:text-prpl border-b">Astana</p>
          <p class="mx-1 p-2 cursor-pointer hover:text-prpl border-b">Uralsk</p>
          <p class="mx-1 p-2 cursor-pointer hover:text-prpl">Pavlodar</p>
        </div>
        <p class="hover:text-prpl transition"><router-link to="/products">Catalogue<i class="fas fa-search ml-3 text-sm"></i></router-link></p>
        <p @click="changeM()" class="cursor-pointer hover:text-prpl transition">Log in</p>

        <button @click="changeSc()" class="text-xl hover:text-prpl transition"><i class="fas fa-balance-scale"></i></button>
        <div v-if="showCompared === 1" class="scndDrop w-trn p-2 bg-neutral-100 text-center rounded-lg"><p class="text-prpl font-semibold">Compare</p>
          <p>...</p></div>
        <button @click="changeF()" class="text-xl hover:text-prpl transition"><i class="far fa-heart"></i></button>
        <div v-if="showFavorites === 1" class="thrdDrop w-trn p-2 bg-neutral-100 text-center rounded-lg"><p class="text-prpl font-semibold">Favorites</p>
          <p>...</p></div>
        <button @click="changeC()" class="text-xl hover:text-prpl transition"><i class="fas fa-shopping-cart"></i></button>
        <div v-if="showCart === 1" class="frthDrop w-trn p-2 bg-neutral-100 text-center rounded-lg"><p class="text-prpl font-semibold">Cart</p>
        <!-- <p v-if="" class="my-2">Your cart is empty</p> --> <Cart /></div>
      </div>
    </div>

    <div v-if="showModal === 1">
      <div class="py-10 transition duration-150 ease-in-out z-10 absolute top-0 right-0 bottom-0 left-0" :class="{ 'blackbg' : showModal === 1}" id="modal">
        <div v-if="logIn === 1" role="login" class="container mx-auto w-11/12 md:w-2/3 max-w-lg">
          <div class="relative py-8 px-5 md:px-10 bg-white rounded-lg mt-14">
            <div class="w-full flex justify-start mb-4"><p class="font-bold text-prpl font-lg">ma<span>Ғ</span>azin</p></div>
            <h1 class="font-semibold tracking-normal leading-tight mb-3"><i class="fas fa-unlock mr-3 text-prpl"></i>Log in</h1>
            <label for="email" class="text-sm font-semibold leading-tight tracking-normal">Enter your email</label>
            <input id="email" class="mb-4 mt-2 focus:outline-none focus:border focus:border-prpl w-full h-10 flex items-center pl-3 text-sm rounded-lg border border-gray-300" placeholder="Jer@email.com" />
            <label for="password" class="text-sm font-semibold leading-tight tracking-normal">Enter your password</label>
            <input id="password" class="mb-4 mt-2 focus:outline-none focus:border focus:border-prpl w-full h-10 flex items-center pl-3 text-sm rounded-lg border border-gray-300" placeholder="123" />
            <div class="flex items-center justify-start w-full">
              <button class="focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-prpl transition duration-150 ease-in-out hover:bg-lghtprpl bg-prpl rounded text-white px-8 py-2 text-sm">
              Log in
              </button>
              <!-- <button class="focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-neutral-300 ml-3 bg-neutral-100 transition duration-150 text-gray-600 ease-in-out hover:border-gray-400 hover:bg-black/10 rounded px-8 py-2 text-sm"
                onclick="modalHandler()">Cancel
              </button> -->
            <button @click="goToRegistration()" class="ml-3 text-prpl hover:text-lghtprpl focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-lghtprpl duration-150 ease-in-out hover:bg-lgprtwo rounded px-8 py-2 text-sm transition">Registration</button>
            </div>
            <button
              class="cursor-pointer absolute top-0 right-0 mt-4 mr-5 text-gr hover:text-lggr transition duration-150 ease-in-out rounded focus:ring-2 focus:outline-none focus:ring-lggr px-2"
              onclick="modalHandler()" @click="showModal = 0" aria-label="close modal" role="button"><i class="fas fa-times"></i>
            </button>
          </div>
        </div>

        <div v-if="register === 1" role="registration" class="container mx-auto w-11/12 md:w-2/3 max-w-lg">
          <div class="relative py-8 px-5 md:px-10 bg-white rounded-lg mt-14">
            <div class="w-full flex justify-start mb-4"><p class="font-bold text-prpl font-lg">ma<span>Ғ</span>azin</p></div>
            <h1 class="font-semibold tracking-normal leading-tight mb-3"><i class="fas fa-lock mr-3 text-prpl"></i>Registration</h1>
            <label for="name" class="text-sm font-semibold leading-tight tracking-normal">Enter your name</label>
            <input id="name" class="mb-4 mt-2 focus:outline-none focus:border focus:border-prpl w-full h-10 flex items-center pl-3 text-sm rounded-lg border border-gray-300" placeholder="Jer" />
            <label for="surname" class="text-sm font-semibold leading-tight tracking-normal">Enter your surname</label>
            <input id="surname" class="mb-4 mt-2 focus:outline-none focus:border focus:border-prpl w-full h-10 flex items-center pl-3 text-sm rounded-lg border border-gray-300" placeholder="Khan" />
            <label for="email" class="text-sm font-semibold leading-tight tracking-normal">Enter your email</label>
            <input id="email" class="mb-4 mt-2 focus:outline-none focus:border focus:border-prpl w-full h-10 flex items-center pl-3 text-sm rounded-lg border border-gray-300" placeholder="Jer@email.com" />
            <label for="phone" class="text-sm font-semibold leading-tight tracking-normal">Enter your mobile phone</label>
            <input id="phone" class="mb-4 mt-2 focus:outline-none focus:border focus:border-prpl w-full h-10 flex items-center pl-3 text-sm rounded-lg border border-gray-300" placeholder="8-(701)-000-00-00" />
            <label for="password" class="text-sm font-semibold leading-tight tracking-normal">Enter your password</label>
            <input id="password" class="mb-4 mt-2 focus:outline-none focus:border focus:border-prpl w-full h-10 flex items-center pl-3 text-sm rounded-lg border border-gray-300" placeholder="123" />
            <div class="flex items-center justify-start w-full">
              <button class="focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-prpl transition duration-150 ease-in-out hover:bg-lghtprpl bg-prpl rounded text-white px-8 py-2 text-sm">
              Register
              </button>
              <!-- <button class="focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-neutral-300 ml-3 bg-neutral-100 transition duration-150 text-gray-600 ease-in-out hover:border-gray-400 hover:bg-black/10 rounded px-8 py-2 text-sm"
                onclick="modalHandler()">Cancel
              </button> -->
            <button @click="goTologIn()" class="ml-3 text-prpl hover:text-lghtprpl focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-lghtprpl duration-150 ease-in-out hover:bg-lgprtwo rounded px-8 py-2 text-sm transition">Log in</button>
            </div>
            <button
              class="cursor-pointer absolute top-0 right-0 mt-4 mr-5 text-gr hover:text-lggr transition duration-150 ease-in-out rounded focus:ring-2 focus:outline-none focus:ring-lggr px-2"
              onclick="modalHandler()" @click="showModal = 0" aria-label="close modal" role="button"><i class="fas fa-times"></i>
            </button>
          </div>
        </div>
      </div>
    </div>

      <RouterView />
  </div>
</template>

<script>
import Cart from '@/views/Cart.vue'
export default {
name: "HeaderSet",
 components: {
    Cart
  },
data() {
  return {
    showFavorites: 0,
    showCart: 0,
    showModal: 0,
    showTown: 0,
    logIn: 0,
    register: 0,
    covered: 0
  }
},
methods : {
    changeSc() {
      if(this.showCompared === 0) {
        this.showCompared = 1
        this.showFavorites = 0
        this.showCart = 0
        this.showModal = 0
        this.showTown = 0
      } else {
        this.showCompared = 0
      }
    },
   changeF() {
      if(this.showFavorites === 0) {
        this.showFavorites = 1
        this.showCart = 0
        this.showModal = 0
        this.showTown = 0
        this.showCompared = 0
      } else {
        this.showFavorites = 0
      }
    },
    changeC() {
      if(this.showCart === 0) {
        this.showCart = 1
        this.showFavorites = 0
        this.showModal = 0
        this.showTown = 0
        this.showCompared = 0
      } else {
        this.showCart = 0
      }
    },
    changeM() {
      if(this.showModal === 0) {
        this.showModal = 1
        this.logIn = 1
        this.showFavorites = 0
        this.showCart = 0
        this.showTown = 0
        this.showCompared = 0
        this.register = 0
      } else {
        this.showModal = 0
      }
    },
    changeT() {
      if(this.showTown === 0) {
        this.showTown = 1
        this.showFavorites = 0
        this.showCart = 0
        this.showModal = 0
        this.showCompared = 0
      } else {
        this.showTown = 0
      }
    },
    goToRegistration() {
      if(this.register === 0) {
        this.register = 1
        this.logIn = 0
      } else {
        this.register = 0
      }
    },
    goTologIn() {
      if(this.logIn === 0) {
        this.logIn = 1
        this.register = 0
      } else {
        this.logIn = 0
      }
    }
}
}
</script>