<script setup>
import data from "@/assets/data.json"
import { ref, defineEmits } from 'vue'
const productsList = data.productsList
const itemSelected = ref({})
const emit = defineEmits(['productData'])

function getProduct(product) {
  itemSelected.name = product.name
  itemSelected.engName = product.engName
  itemSelected.price = product.price
  emit('productData', itemSelected)
 }

</script>

<template>
  <div class="p-2">
    <button  v-for="product in productsList" :key="product.name" class="btn form-control p-0" 
    @click="getProduct(product)" >
      <div class="border border-outline-primary px-3 py-2 text-start">
        <p class="mb-1">{{ product.name }}</p>
        <div class="d-flex justify-content-between mb-0">
          <p class="mb-0 me-2">{{ product.engName }} </p>
          <p class="mb-0 text-nowrap ">NT {{ product.price }}元</p>
        </div>
      </div>
    </button>
  </div>
  
</template>

<style>
.active {
  background-color: #007bff;
}
</style>