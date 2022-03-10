<template>
	<main class="container">
		<Home>
		</Home>
	</main>
</template>

<script>

import Home    from './components/Home.vue'

export default {
	name: 'App',
	components: {
    Home: Home
	},

	data() {
		return {

		}
	},
}
</script>
<style>
	@import url("https://fonts.googleapis.com/css2?family=Nunito:wght@300&display=swap");
  
	* {
		font-family: 'Nunito', sans-serif;
		box-sizing: border-box;
		padding:0;
		margin:0;
		outline: none;
	}
  
	.container {
		height: auto;
		width: 100%;
		flex-direction: column;
		display: flex;
		justify-content: center;
		align-items: center;
    gap: 2rem;
	}
</style>
