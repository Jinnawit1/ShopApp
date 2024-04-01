<script setup>
import { onMounted, ref, watch } from 'vue'
import Userlayout from '../layout/Userlayout.vue'
const listpro = JSON.parse(localStorage.getItem('listpro')) || []

const addproduct = (index) => {
  listpro[index].amount++
  listpro[index].price += listpro[index].initialPrice

  localStorage.setItem('listpro', JSON.stringify(listpro))

  console.log(listpro)
  window.location.reload()
}

const sumPrice = ref(listpro.reduce((sum, item) => sum + item.price, 0))
const sumPricecal = ref(listpro.reduce((sum, item) => sum + item.price, 0))
const sumAmount = listpro.reduce((sum, item) => sum + item.amount, 0)
const fixamount = ref(false)
const percent = ref(false)
const percentitem = ref(false)
const point = ref(false)
const customerpoint = ref(0)
const onsubmit = ref(true)
const spacial = ref(false)
let subtractedValue = 0
let subtractedValue1 = 0
let subtractedValue3 = 0

watch(fixamount, (newValue) => {
  if (newValue) {
    sumPrice.value -= 50
    console.log(sumPrice.value)
  } else if (!newValue) {
    sumPrice.value += 50
  }
})
watch(percent, (newValue) => {
  if (newValue) {
    subtractedValue = (sumPricecal.value * 10) / 100
    sumPrice.value -= subtractedValue
  } else if (!newValue) {
    sumPrice.value += subtractedValue
    subtractedValue = 0
  }
})
watch(percentitem, (newValue) => {
  if (newValue) {
    subtractedValue1 = (listpro[0].price * 15) / 100
    sumPrice.value -= subtractedValue1
  } else if (!newValue) {
    sumPrice.value += subtractedValue1
    subtractedValue1 = 0
  }
})
const submitpoint = (newpoint) => {
  let sumpoint = (sumPricecal.value * 20) / 100
  if (newpoint < sumpoint) {
    sumPrice.value -= newpoint
    onsubmit.value = false
  } else {
    alert('more than 20%')
  }
}
watch(spacial, (newValue) => {
  let discount = Math.floor(sumPrice.value / 300) * 40
  if (newValue) {
    subtractedValue3 = discount
    sumPrice.value -= subtractedValue3
  } else if (!newValue) {
    sumPrice.value += subtractedValue3
    subtractedValue3 = 0
  }
})
listpro.sumprice = sumPrice
listpro.sumAmount = sumAmount
console.log(listpro)

// Save listpro to local storage
</script>
<template>
  <Userlayout>
    <h1 class="text-3xl font-bold m- 4">Shoping Cart</h1>
    <div class="grid grid-cols-2">
      <div v-if="listpro.length == 0" class="grid grid-cols-2 p-4 bg-base-200"></div>
      <div
        v-else
        v-for="(item, index) in listpro"
        :key="item.id"
        class="grid grid-cols-2 p-4 bg-base-200"
      >
        <figure style="height: 300px; overflow: hidden">
          <img :src="item.img" style="width: 100%; height: 100%; object-fit: cover" />
        </figure>

        <div>
          <div class="grid grid-cols-2">
            <div>
              <div>productname</div>
              <div>amount</div>
              <div>price</div>
            </div>
            <div>
              <div>{{ item.name }}</div>
              <div class="grid grid-cols-2">
                <p>{{ item.amount }}</p>
                <button
                  @click="addproduct(index)"
                  class="btn w-10 btn-xs size:sm btn-outline btn-info"
                >
                  +
                </button>
              </div>
              <div>{{ item.price }}</div>
            </div>
          </div>
        </div>
      </div>
      <div class="bg-base-200 p-5 divide-y divide-black">
        <div class="text-xl pb-3">Order Summary</div>

        <div class="grid grid-cols-2">
          <div>
            <div>description</div>
            <div>price</div>
            <div class="label-text pb-4">Fixed amount</div>
            <div class="label-text pb-4">Percentage discount</div>
            <div class="label-text pb-4">Percentage discount by item category</div>
            <div class="label-text pb-4">Discount by points</div>
            <div class="label-text pb-4">Special campaigns</div>
          </div>
          <div>
            <div class="">{{ listpro.sumprice }}</div>

            <div class="">{{ listpro.sumAmount }}</div>
            <div v-if="percent == false" class="pb-1">
              <input v-model="fixamount" type="checkbox" class="toggle" />
            </div>
            <div v-else>
              <input v-model="fixamount" disabled type="checkbox" class="toggle" />
            </div>
            <div v-if="fixamount == false" class="pb-1">
              <input v-model="percent" type="checkbox" class="toggle" />
            </div>
            <div v-else>
              <input v-model="fixamount" disabled type="checkbox" class="toggle" />
            </div>
            <div v-if="point == false" class="pb-1">
              <input v-model="percentitem" type="checkbox" class="toggle" />
            </div>
            <div v-else>
              <input v-model="fixamount" disabled type="checkbox" class="toggle" />
            </div>
            <div v-if="percentitem == false" class="pb-1">
              <input v-model="point" type="checkbox" class="toggle" />
              <input
                v-if="point == true && onsubmit == true"
                v-model="customerpoint"
                type="number"
              />
              <button
                v-if="point == true && onsubmit == true"
                @click="submitpoint(customerpoint)"
                class="btn"
              >
                enter
              </button>
            </div>
            <div v-else>
              <input v-model="point" disabled type="checkbox" class="toggle" />
            </div>
            <div>
              <input v-model="spacial" type="checkbox" class="toggle" />
            </div>
          </div>
        </div>
      </div>
    </div>
  </Userlayout>
</template>
