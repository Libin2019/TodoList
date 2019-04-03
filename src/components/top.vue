<template>
	<h1>{{ message }}</h1>
</template>

<script>
	export default {
		name:'top',
		data() {
			return {
				message:'Do what you love'
			};
		}
	}
</script>

<style scoped="scoped">
	h1{
		color: black;
		font-size: 4em;
		text-align: center;
	}

</style>
