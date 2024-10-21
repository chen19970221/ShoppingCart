<script setup>
import { reactive } from 'vue'
import Products from './components/Products.vue'
import Cart from './components/Cart.vue'
import Details from './components/Details.vue'
const product = reactive({
  name: '',
  engName: '',
  price: '',
  drinkQuantity: '',
  sugarAnswer: '',
  iceAnswer: '',
  toppingsAnswer: '',
  memo: ''
});



const productData = (item) => {
  product.name = item.name
  product.engName = item.engName
  product.price = item.price
}

const detailData = (item) => { 
  console.log(product)
  console.log(item)
  product.drinkQuantity = item.drinkQuantity
  product.sugarAnswer = item.sugar
  product.iceAnswer = item.ice
  product.toppingsAnswer = item.toppings
  product.memo = item.memo
  console.log(product)
}




</script>

<template>
  <div class="container">
    <div class="row">
      <div class="col-12 col-sm-6 col-md-4">
        <Products @productData="productData"/>
      </div>
      <div class="col-12 col-sm-6 col-md-8">
        <Details @detailData="detailData"/>
        <Cart :product="product"/>
      </div>
    </div>
  </div>
</template>

<style>

</style>
