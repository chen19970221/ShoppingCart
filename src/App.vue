<script setup>
import { ref, reactive } from 'vue'
import Products from './components/Products.vue'
import Cart from './components/Cart.vue'
import Details from './components/Details.vue'
const cartList = reactive([]) 
const product = {}


const productData = (item) => {
  product.name = item.name
  product.engName = item.engName
  product.price = item.price
}

const detailData = (item) => { 
  console.log(item)
  product.drinkQuantity = item.drinkQuantity
  product.sugarAnswer = item.sugarAnswer
  product.iceAnswer = item.iceAnswer
  product.toppingsAnswer = item.toppingsAnswer
  product.memo = item.memo
  console.log(product)
  var newProduct = {};
  for (var key in product) {
    newProduct[key] = product[key];
  }
  cartList.push(newProduct)
  newProduct = {}  
  console.log(cartList)
  countTotal(cartList)

}

function countTotal(cartList) {
  const subTotal = cartList.price * cartList.drinkQuantity
  console.log(subTotal)
  // total.value = cartList.reduce((total, item) => total + (item.price * item.drinkQuantity), 0)
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
        <Cart :cartList="cartList"/>
      </div>
    </div>
  </div>
</template>

<style>

</style>
