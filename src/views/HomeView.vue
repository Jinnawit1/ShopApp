<script setup>
import { reactive } from 'vue'
import layout from '../layout/Userlayout.vue'
import { list } from 'postcss'
const product = reactive([
  {
    name: 'T-shirt',
    img: 'https://img.freepik.com/free-psd/simple-black-men-s-tee-mockup_53876-57893.jpg?size=626&ext=jpg&ga=GA1.1.1224184972.1711843200&semt=ais',
    price: 350,
    initialPrice: 350,
    amount: 1
  },
  {
    name: 'Hat',
    img: 'https://img.freepik.com/free-psd/cap-mockup_1310-495.jpg',
    price: 250,
    initialPrice: 250,
    amount: 1
  },
  {
    name: 'Hoodie',
    img: 'https://unblast.com/wp-content/uploads/2021/10/Simple-Hoodie-Mockup-2.jpg',
    price: 700,
    initialPrice: 700,
    amount: 1
  },
  {
    name: 'Watch',
    img: 'https://img.freepik.com/free-photo/closeup-shot-golden-watch-isolated_181624-28492.jpg?size=626&ext=jpg&ga=GA1.1.1224184972.1711843200&semt=ais',
    price: 850,
    initialPrice: 850,
    amount: 1
  },
  {
    name: 'Bag',
    img: 'https://images.pexels.com/photos/1152077/pexels-photo-1152077.jpeg?cs=srgb&dl=pexels-ge-yonk-1152077.jpg&fm=jpg',
    price: 640,
    initialPrice: 640,
    amount: 1
  },
  {
    name: 'Belt:',
    img: 'https://img.freepik.com/free-photo/leather-belt_74190-2615.jpg?size=626&ext=jpg&ga=GA1.1.1224184972.1711843200&semt=ais',
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
  <layout>
    <!-- ------------------- -->
    <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-4">
      <div v-for="item in product" :key="item.id" class="card w-full bg-base-100 shadow-xl">
        <figure style="height: 300px; overflow: hidden">
          <img :src="item.img" style="width: 100%; height: 100%; object-fit: cover" />
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
