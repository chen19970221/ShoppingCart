<script setup>
import data from "@/assets/data.json"
import { ref, defineEmits } from "vue"
const sugarAnswer = ref('')
const iceAnswer = ref('')
const toppingsAnswer = ref('')
const drinkQuantity = ref(1)
const memo = ref('')
const emit = defineEmits(['detailData'])

function getDetails(drinkQuantity, sugarAnswer, iceAnswer, toppingsAnswer, memo) { 
  const details = {}
  details.drinkQuantity = drinkQuantity
  details.sugar = sugarAnswer
  details.ice = iceAnswer
  details.toppings = toppingsAnswer
  details.memo = memo
  console.log(details)
  emit('detailData', details)
}

</script>

<template>
  <div class="p-2">
    <form class="p-3 border">
      <!-- quantity -->
      <div class="mb-3">
        <label for="quantity" class="form-label">數量</label>
        <input type="text" id="quantity" class="form-control" v-model="drinkQuantity">
      </div>

      <!-- ice -->
      <div class="mb-3">
        <p class="mb-1">冰塊*</p>
        <span class="me-2" v-for=" ice in data.iceType" :key="ice">
          <input type="radio" :id="ice" class="me-1" v-model="iceAnswer" :value="ice" >
          <label :for="ice">{{ ice }}</label>
        </span>
      </div>

      <!-- sugar -->
      <div class="mb-3">
        <p class="mb-1">甜度*</p>
        <span class="me-2" v-for=" sugar in data.sugarType" :key="sugar">
          <input type="radio" :id="sugar" class="me-1" v-model="sugarAnswer" :value="sugar" >
          <label :for="sugar">{{ sugar }}</label>
        </span>
      </div>

      <!-- toppings -->
      <div class="mb-3">
        <p class="mb-1">加料</p>
        <span class="me-2" v-for=" topping in data.toppingsType" :key="topping">
          <input type="checkbox" :id="topping" class="me-1" v-model="toppingsAnswer" :value="topping" >
          <label :for="topping">{{ topping }}</label>
        </span>
      </div>

      <!-- memo -->
      <div class="mb-3">
        <label for="memo" class="form-label">備註</label>
        <textarea id="memo" class="form-control" rows="3" v-model="memo"></textarea>
      </div>

      <!-- submit -->
      <div class="row g-2">
        <div class="col-12 col-sm-6">
          <button type="button" class="btn btn-outline-primary form-control">取消</button>
        </div>
        <div class="col-12 col-sm-6">
          <button type="button" class="btn btn-primary form-control" 
            @click="getDetails(drinkQuantity, sugarAnswer, iceAnswer, toppingsAnswer, memo)">
            送出
          </button>
        </div>
      </div>


    
    </form>
  </div>
</template>

<style></style>