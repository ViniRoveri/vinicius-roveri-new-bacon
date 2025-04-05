<script setup>
import { RouterLink } from 'vue-router';

   defineProps({
      deleteFunction: Function,
      user: Object
   })
</script>

<template>
   <div class="card">
      <img class="userPicture" :src="user.urlPicture">

      <div class="userInfo">
         <p>#{{ user.id }}</p>
         <p>{{ user.name }}</p>
         <p>{{ user.email }}</p>
      </div>

      <div class="actions">
         <RouterLink :to="`/user/${user.id < 7 ? user.id : 1}`">
            <i class="ri-edit-box-line"></i>
         </RouterLink>
         
         <button @click="deleteFunction(user.id)" type="button">
            <i class="ri-delete-bin-6-line"></i>
         </button>

         <RouterLink :to="`/user/${user.id < 7 ? user.id : 1}`">
            <i class="ri-eye-line"></i>
         </RouterLink>
      </div>
   </div>
</template>

<style scoped>
   .card{
      align-items: center;
      background-color: #F7F7F7;
      border-radius: 5px;
      display: flex;
      gap: 24px;
      justify-content: space-between;
      padding: 20px 30px;
   }

   .userPicture{
      border-radius: 5px;
      height: 80px;
      width: 80px;
   }

   .userInfo{
      color: #797979;
      display: flex;
      flex-direction: column;
      flex-grow: 1;
      gap: 4px;
      justify-content: space-between;
   }

   .userInfo>p:not(:nth-child(2)){
      color: #797979;
   }

   .userInfo>p:nth-child(2){
      font-size: 18px;
      font-weight: 600;
   }
   
   .actions{
      display: flex;
      gap: 16px;
      justify-content: space-between;
   }

   .actions i {
      color: #797979;
      font-size: 20px;
   }
</style>