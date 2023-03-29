<script setup>
import { RouterView } from 'vue-router'
</script>

<script>

export default {
	name: 'App',
	data() {
		return {
			
		}
	},
	methods: {
		start() {
			console.log('start')
		},
		stop() {
			console.log('stop')
		},
		reset() {
			console.log('reset')
		},
	}
}

</script>

<template>
  <header>
    <!-- <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" /> -->

    
      <!-- <HelloWorld msg="You did it!" /> -->
		
      <!-- <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </nav> -->
  </header>

  <RouterView />
</template>

<style lang="sass" scoped>

	#app
		grid-template-columns: 1fr

	header
		line-height: 1.5
		max-height: 100vh

	@media (min-width: 1024px) 
		.wrapper 
			display: flex
			justify-content: center

		header 
			display: flex
			place-items: center
			padding-right: calc(var(--section-gap) / 2)
</style>
