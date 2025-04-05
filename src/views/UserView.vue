<script setup>
	import axios from 'axios';
	import { ref, onMounted } from 'vue';
	import { useRoute } from 'vue-router/composables';
	import Title from '@/components/Title.vue'
	import DefaultButton from '@/components/DefaultButton.vue'
	import InfoField from '@/components/InfoField.vue'
import { RouterLink } from 'vue-router';

	const route = useRoute()
   const user = ref({})

   onMounted(async () => {
		const req = await axios.get(`https://reqres.in/api/users/${route.params.id}`)

		user.value =  {
			id: req.data.data.id,
			firstName: req.data.data.first_name,
			lastName: req.data.data.last_name,
			email: req.data.data.email,
			urlPicture: req.data.data.avatar,
			supportLink: req.data.support.url,
			description: req.data.support.text
		}
	})
</script>

<template>
	<main>
		<header>
			<Title>#{{ user.id }}</Title>
			
			<DefaultButton color="gray">
				<RouterLink to="/">
					Voltar
				</RouterLink>
			</DefaultButton>
		</header>

		<div class="userNames">
			<img class="userPicture" :src="user.urlPicture">

			<InfoField label="Primeiro nome" :value="user.firstName"/>

			<InfoField label="Último nome" :value="user.lastName"/>
		</div>

		<div class="userInfos">
			<InfoField label="Endereço de e-mail" :value="user.email"/>

			<InfoField label="Link do avatar" :value="user.urlPicture"/>

			<InfoField label="Link de suporte" :value="user.supportLink"/>
			
			<InfoField label="Descrição do usuário" :value="user.description"/>
		</div>
	</main>
</template>

<style scoped>
	.userNames{
		align-items: center;
		display: flex;
		gap: 34px;
		margin-bottom: 30px;
	}

	.userPicture{
		border-radius: 5px;
		height: 120px;
		width: 120px;
	}

	.userInfos{
		display: flex;
		flex-direction:column;
		gap: 20px;
	}
</style>