<script setup>
import data from "@/assets/data.json"
import { ref, defineEmits } from "vue"
const sugarAnswer = ref('')
const iceAnswer = ref('')
const toppingsAnswer = ref([])
const drinkQuantity = ref(1)
const memo = ref('')
const emit = defineEmits(['detailData'])
const props = defineProps(['product','productData'])

function getDetails(drinkQuantity, sugarAnswer, iceAnswer, toppingsAnswer, memo) { 
  console.log(sugarAnswer,sugarAnswer.value)
  const details = {}
  details.drinkQuantity = drinkQuantity
  details.sugarAnswer = sugarAnswer !== ''? sugarAnswer:'全糖'
  details.iceAnswer = iceAnswer !== '' ? iceAnswer : '正常冰'
  details.toppingsAnswer = toppingsAnswer
  details.memo = memo
  console.log(details)
  emit('detailData', details)
  drinkQuantity.value = 1
  sugarAnswer.value = '';
  iceAnswer.value = '';
  toppingsAnswer.value = [];
  memo.value = '';
}

function cancelDetails() {
  drinkQuantity.value = 1;
  sugarAnswer.value = '';
  iceAnswer.value = '';
  toppingsAnswer.value = [];
  memo.value = '';
  console.log(sugarAnswer.value, iceAnswer.value); 
}

</script>

<template>

  <!-- <div v-if="!props.product.hasOwnProperty('name')" class="position-absolute text-white d-flex align-items-center justify-content-center" style="background-color: rgba(0, 0, 0, 0.65); top:8px; bottom:-76px;  width:52%;">請先選擇飲品</div> -->
  <div class="p-2">
    <form class="p-3 border">
      <!-- quantity -->
      <div class="mb-3">
        <label for="quantity" class="form-label">數量</label>
        <input type="number" id="quantity" class="form-control" v-model.number="drinkQuantity">
        {{ typeof drinkQuantity }}
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
        <span class="me-2" v-for=" toppings in data.toppingsType" :key="toppings">
          <input type="checkbox" :id="toppings" class="me-1" v-model="toppingsAnswer" :value="toppings" >
          <label :for="toppings">{{ toppings }}</label>
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
          <button type="button" class="btn btn-outline-primary form-control" 
            @click="cancelDetails">
            取消
          </button>
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