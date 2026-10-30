<template>
  <div class="gridd">
    <span> {{ value.name }}</span> 
    <span>{{ value.current_price }}</span>
    <span>{{ value.price_change_percentage_24h >= 0 ? '⬆' : '↓' }}</span>
    <span :style="{ color: value.price_change_percentage_24h >= 0 ? '#10b981' : '#ef4444' }">
      {{ value.price_change_percentage_24h?.toFixed(2) }} %
    </span>

 
  </div>
</template>

<script setup lang="ts"> 

import type { Coin } from "./Home.vue"

const props = defineProps<{
  value: Coin
}>()


</script>

<style lang="scss" scoped>
.gridd {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 5px;
}




</style>
