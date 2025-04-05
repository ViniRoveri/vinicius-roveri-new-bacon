<script setup>
import { ref } from 'vue';
import { RouterLink } from 'vue-router';

   const props = defineProps({
      deleteFunction: Function,
      editFunction: Function,
      user: Object
   })

   const isEditMode = ref(false)
   const newUsername = ref(props.user.name)

   const exitEditMode = () => {
      isEditMode.value = false
      newUsername.value = props.user.name
   }

   const editUser = () => {
      if(!newUsername.value) return

      isEditMode.value = false
      props.editFunction(props.user.id, newUsername)
   }
</script>

<template>
   <div class="card">
      <img class="userPicture" :src="user.urlPicture">

      <div class="userInfo">
         <p class="userId">#{{ user.id }}</p>

         <p v-if="!isEditMode" class="userName">{{ user.name }}</p>
         <input v-else class="userName" v-model="newUsername" type="text">

         <p class="userEmail">{{ user.email }}</p>
      </div>

      <div v-if="!isEditMode" class="actions">
         <button  @click="isEditMode = true" type="button">
            <i class="ri-edit-box-line"></i>
         </button>
         
         <button @click="deleteFunction(user.id)" type="button">
            <i class="ri-delete-bin-6-line"></i>
         </button>

         <RouterLink :to="`/user/${user.id}`">
            <i class="ri-eye-line"></i>
         </RouterLink>
      </div>
      <div v-else class="actions">
         <button  @click="editUser" type="button">
            <i class="ri-check-line"></i>
         </button>

         <button  @click="exitEditMode" type="button">
            <i class="ri-close-line"></i>
         </button>
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

   .userId, .userEmail{
      color: #797979;
   }

   .userName{
      font-size: 18px;
      font-weight: 600;
   }

   input.userName{
      border: 1px solid #797979;
      border-radius: 5px;
      padding: 0 8px;
   }
   
   .actions{
      display: flex;
      gap: 16px;
      justify-content: end;
   }

   .actions i {
      color: #797979;
      font-size: 20px;
   }
</style>