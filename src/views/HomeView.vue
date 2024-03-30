<script setup>
import { reactive } from 'vue'
import layout from '../layout/Userlayout.vue'
import { list } from 'postcss'
const product = reactive([
  {
    name: 'T-shirt',
    img: 'https://daisyui.com/images/stock/photo-1606107557195-0e29a4b5b4aa.jpg',
    price: 350,
    initialPrice: 350,
    amount: 1
  },
  {
    name: 'Hat',
    img: 'https://daisyui.com/images/stock/photo-1606107557195-0e29a4b5b4aa.jpg',
    price: 250,
    initialPrice: 250,
    amount: 1
  },
  {
    name: 'Hoodie',
    img: 'https://daisyui.com/images/stock/photo-1606107557195-0e29a4b5b4aa.jpg',
    price: 700,
    initialPrice: 700,
    amount: 1
  },
  {
    name: 'Watch',
    img: 'https://daisyui.com/images/stock/photo-1606107557195-0e29a4b5b4aa.jpg',
    price: 850,
    initialPrice: 850,
    amount: 1
  },
  {
    name: 'Bag',
    img: 'https://daisyui.com/images/stock/photo-1606107557195-0e29a4b5b4aa.jpg',
    price: 640,
    initialPrice: 640,
    amount: 1
  },
  {
    name: 'Belt:',
    img: 'https://daisyui.com/images/stock/photo-1606107557195-0e29a4b5b4aa.jpg',
    price: 230,
    initialPrice: 230,
    amount: 1
  }
])
const listpro = JSON.parse(localStorage.getItem('listpro')) || []

const addtocart = (product) => {
  const findproductindex = listpro.findIndex((item) => {
    return item.name === product.name
  })
  console.log(findproductindex)
  if (findproductindex < 0) {
    listpro.push(product)
  } else {
    alert('already have this item')
  }

  localStorage.setItem('listpro', JSON.stringify(listpro))
  // Save listpro to local storage
}
</script>

<template>
  <layout
    ><div class="hero h-screen bg-base-200">
      <div class="hero-content text-center">
        <div class="max-w-md">
          <h1 class="text-5xl font-bold">Hello there</h1>
          <p class="py-6">
            Provident cupiditate voluptatem et in. Quaerat fugiat ut assumenda excepturi
            exercitationem quasi. In deleniti eaque aut repudiandae et a id nisi.
          </p>
          <button class="btn btn-primary">Get Started</button>
        </div>
      </div>
    </div>
    <!-- ------------------- -->
    <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-4">
      <div v-for="item in product" :key="item.id" class="card w-full bg-base-100 shadow-xl">
        <figure>
          <img :src="item.img" />
        </figure>
        <div class="card-body">
          <h2 class="card-title">{{ item.name }}</h2>
          <p>{{ item.price }} Bath</p>
          <div class="card-actions justify-end">
            <button @click="addtocart(item)" class="btn btn-primary">Buy Now</button>
          </div>
        </div>
      </div>
    </div>
  </layout>
</template>
