<script setup>
	import axios from 'axios';
	import { ref, onMounted } from 'vue';
	import { useRoute } from 'vue-router/composables';
	
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

</template>