<script setup>
import data from "@/assets/data.json"
import {  defineEmits, reactive } from 'vue'
const productsList = data.productsList
const itemSelected = reactive({})
const emit = defineEmits(['productData'])

function getProduct(product) {
  itemSelected.name = product.name
  itemSelected.engName = product.engName
  itemSelected.price = product.price
  console.log(itemSelected.name)
  emit('productData', itemSelected)
 }

</script>

<template>
  <div class="p-2">
    <button  v-for="product in productsList" :key="product.name" class="btn form-control p-0" 
    @click="getProduct(product)" :class="{ 'active': itemSelected.name === product.name}">
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
  background-color: var(--bs-primary) !important;
  border-color: var(--bs-primary) !important;
  color: white !important; 
}
</style>