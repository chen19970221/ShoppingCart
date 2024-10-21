<script setup>
import { defineProps } from "vue"

const props = defineProps({
  product: Object
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
          <tr>
            <td>
              {{  props.product.name }}
              <br>
              <span class="text-secondary text-opacity-75">{{ props.product.memo }}</span>
            </td>
            <td>{{ props.product.ice }}</td>
            <td>{{ props.product.sugar }}</td>
            <td>{{ props.product.toppings }}</td>
            <td class="text-end pe-3">{{ props.product.price }}</td>
            <td>{{ props.product.quantity }}</td>
            <td></td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>