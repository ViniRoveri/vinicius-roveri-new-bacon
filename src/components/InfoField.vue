<script setup>
   defineProps({
      isBig: Boolean,
      label: String,
      value: String
   })
</script>

<template>
   <div :style="isBig ? 'width: 100%' : ''">
      <p class="label">{{ label }}</p>
      <p class="value">{{ value }}</p>
   </div>
</template>

<style scoped>
   .label{
      color: #797979;
      font-size: 14px;
      margin-bottom: 8px;
   }

   .value{
      font-weight: 600;
   }
</style>