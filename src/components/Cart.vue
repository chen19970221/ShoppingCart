<script setup>
import { computed, defineProps } from "vue"

const props = defineProps({
  cartList: Array
});

const orderId = new Date().getTime()

const total = computed(() => {
  return props.cartList.reduce((sum, item) => {
    return sum + item.price * item.drinkQuantity;
  }, 0);
});



</script>

<template>
  <div class="p-2">
    <div class="p-3 border">
      <table class="table">
        <thead>
          <tr>
            <th scope="row">品項</th>
            <th scope="row">冰塊</th>
            <th scope="row">甜度</th>
            <th scope="row">加料</th>
            <th scope="row">單價</th>
            <th scope="row">數量</th>
            <th scope="row">小計</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for=" item in cartList " :key="orderId">
            <td>
              {{  item.name }}
              <br>
              <span class="text-secondary text-opacity-75">{{ item.memo }}</span>
            </td>
            <td>{{ item.iceAnswer }}</td>
            <td>{{ item.sugarAnswer }}</td>
            <td>
              <span  v-for=" top in item.toppingsAnswer">{{ top }}</span>
            </td>
            <td>{{ item.price }}</td>
            <td>{{ item.drinkQuantity }}</td>
            <td> {{  item.price * item.drinkQuantity }}</td>
          </tr>
        </tbody>
        <tfoot>
          <tr>
            <td colspan="6" class="text-end">總計</td>
            <td>{{ total }}</td>
          </tr>
        </tfoot>
      </table>
    </div>
  </div>
</template>