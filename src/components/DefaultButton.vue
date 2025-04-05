<script setup>
   defineProps({
      color:{
         type: 'black' | 'gray',
         default: 'black'
      },
      isBig: Boolean,
      submit: Boolean
   })
</script>

<template>
   <button :class="color && 'button-' + color" :style="isBig ? 'width: 100%' : ''" :type="submit ? 'submit' : 'button'">
      <slot></slot>
   </button>
</template>

<style scoped>
   button {
      border: none;
      border-radius: 5px;
      font-size: 15px;
      font-weight: 600;
      padding: 18px 40px;
   }

   .button-black{
      background-color: black;
      color: white
   }

   .button-gray{
      background-color: #F7F7F7;
      color: black
   }
</style>