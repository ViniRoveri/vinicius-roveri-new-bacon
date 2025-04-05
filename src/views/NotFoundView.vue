<script setup>
   import Title from '@/components/Title.vue'
   import { RouterLink } from 'vue-router';
</script>

<template>
   <main>
      <Title>Página Não Encontrada</Title>
      <button class="goBackButton" type="button">
         <RouterLink to="/">
            <i class="ri-arrow-left-long-line"></i>
            Voltar para home
         </RouterLink>
      </button>
   </main>
</template>

<style scoped>
   .goBackButton{
      font-size: 20px;
      margin-top: 16px;
   }
</style>