<script setup>
	import axios from 'axios';
	import { ref, onBeforeMount, onBeforeUnmount, onMounted } from 'vue';
	import DefaultButton from '@/components/DefaultButton.vue';
	import Title from '@/components/Title.vue';
	import UserCard from '@/components/UserCard.vue';
	import gsap from 'gsap';
	
	const showForm = ref(false)
	const userFunction = ref('')
	const username = ref('')
	const users = ref([])

	const addUser = () => {
		const lastAddedId = [...users.value].sort((a, b) => b.id - a.id)[0].id
		
		users.value.push({
			id: lastAddedId + 1,
			name: username.value,
			email: username.value.toLowerCase().replaceAll(' ', '.') + '@newbacon.com',
			urlPicture: 'https://ui-avatars.com/api/?name=' + username.value.replaceAll(' ', '+')
		})

		username.value = ''
		userFunction.value = ''
	}

	const editUser = (id, newName) => {
		const user = users.value.find(u => u.id == id)
		const userEmailDomain = user.email.split('@')[1]

		user.name = newName.value
		user.email = `${newName.value.toLowerCase().replaceAll(' ', '.')}@${userEmailDomain}`
	}

   const deleteUser = id => {
      users.value = users.value.filter(u => u.id != id)
   }

   const toggleShowForm = () => {
      showForm.value = !showForm.value
   }

	const animateIntro = () => {
		let tl = gsap.timeline({defaults: {
			duration: 0.25,
			ease: 'power1.inOut'
		}})

		tl.fromTo('header>*:first-child', {
			autoAlpha: 0,
			y: -50
		}, {
			autoAlpha: 1,
			y: 0
		})
		
		tl.fromTo('header>*:nth-child(2)', {
			autoAlpha: 0,
			y: -50
		}, {
			autoAlpha: 1,
			y: 0
		})

		tl.fromTo('ul', {
			autoAlpha: 0,
			x: -50
		}, {
			autoAlpha: 1,
			x: 0
		})
	}

	const animateExit = () => {
		let tl = gsap.timeline({defaults: {
			duration: 0.25,
			ease: 'power1.inOut'
		}})

		tl.to('ul', {
			autoAlpha: 0,
			x: -50
		})
		
		tl.to('header>*:nth-child(2)', {
			autoAlpha: 0,
			y: -50
		})

		tl.to('header>*:first-child', {
			autoAlpha: 0,
			y: -50
		})
	}

	onBeforeMount(async () => {
		const req = await axios.get('https://reqres.in/api/users')

		users.value = req.data.data.map(u => {
			return {
				id: u.id,
				name: `${u.first_name} ${u.last_name}`,
				email: u.email,
				urlPicture: u.avatar
			}
		})
	})

	onMounted(() => {
		animateIntro()
	})

	onBeforeUnmount(() => {
		animateExit()
	})
</script>

<template>
	<main>
		<header>
			<Title>Usuários</Title>

         <div @click="toggleShowForm">
            <DefaultButton v-if="!showForm" color="black">Novo Usuário</DefaultButton>
            <DefaultButton v-else color="gray" >Cancelar</DefaultButton>
         </div>
      </header>
		
      <form autocomplete="off" :style="!showForm ? 'display: none' : ''" @submit.prevent="addUser">
			<div>
				<label for="username" maxlength="40">Nome do usuário</label>
				<input id="username" placeholder="Nome do usuário" required type="text" v-model="username">
			</div>
			
			<div>
				<label for="userFunction">Função do usuário</label>
				<select id="userFunction" required v-model="userFunction">
					<option selected value="">Selecione a função</option>
					<option value="Desenvolvedor">Desenvolvedor</option>
					<option value="Gerente de Projetos">Gerente de Projetos</option>
					<option value="Tech Lead">Tech Lead</option>
					<option value="UI/UX Designer">UI/UX Designer</option>
				</select>
			</div>

			<DefaultButton color="black" isBig submit>Salvar dados do usuário</DefaultButton>
      </form>

		<ul>
			<li v-for="user in users" :key="user.id">
				<UserCard :deleteFunction="deleteUser" :editFunction="editUser" :user="user"/>
			</li>
		</ul>
	</main>
</template>

<style scoped>
	form{
		display: flex;
		flex-direction: column;
		gap: 24px;
		margin-bottom: 44px;
	}

	label{
      font-weight: 600;
   }

   input {
      border: 1px solid #E5E5E5;
      border-radius: 5px;
      margin-top: 12px;
      padding: 18px 20px;
      width: 100%
   }

	select {
      border: 1px solid #E5E5E5;
      border-radius: 5px;
      margin-top: 12px;
      padding: 18px 20px;
      width: 100%
   }

	li {
		margin-bottom: 16px;
	}
</style>
