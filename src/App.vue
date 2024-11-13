<script setup>
import { ref, reactive } from 'vue'
import Products from './components/Products.vue'
import Cart from './components/Cart.vue'
import Details from './components/Details.vue'
const cartList = reactive([]) 
const selectedProduct = reactive({}) // 當筆訂單內容


// 將 product 傳出的飲料種類，放置 selectedProduct
const productData = (item) => {
  selectedProduct.name = item.name
  selectedProduct.engName = item.engName
  selectedProduct.price = item.price
  selectedProduct.defaults = item.defaults
}

// details 傳出的飲料客製化內容
const detailData = (item) => {
  console.log(item)
  selectedProduct.drinkQuantity = item.drinkQuantity
  selectedProduct.sugarAnswer = item.sugarAnswer
  selectedProduct.iceAnswer = item.iceAnswer
  selectedProduct.toppingsAnswer = item.toppingsAnswer
  selectedProduct.memo = item.memo
  const newProduct = { ...selectedProduct }; 
  cartList.push(newProduct);
  Object.keys(selectedProduct).forEach((key) => {
    delete selectedProduct[key];
  });

  console.log(selectedProduct);
}


</script>

<template>

  <div class="container">
    <div class="row">
      <div class="col-12 col-sm-6 col-md-4">
        <Products @productData="productData" :selectedProduct="selectedProduct"/>
      </div>
      <div class="col-12 col-sm-6 col-md-8">
        <Details @detailData="detailData" :selectedProduct="selectedProduct" :productData="productData"/>
        <Cart :cartList="cartList"/>
      </div>
    </div>
  </div>
</template>

<style>

</style>
