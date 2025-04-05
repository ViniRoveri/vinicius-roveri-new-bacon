<script setup>
import { RouterView } from 'vue-router'
</script>

<template>
	<Transition mode="out-in" name="route">
		<RouterView/>
	</Transition>
</template>

<style scoped>
.route-leave-active {
  transition: all 0.25s ease-in-out;
}

.route-leave-to {
  opacity: 0;
  transform: translateX(-100px)
}
</style>