<template>
	<div>
		<p v-for="mix in energy_data" v-bind:key="mix">
			{{ mix.fuel }} - {{ mix.perc }}
		</p>
	</div>
</template>

<script>
export default {
	name: 'energy-graph',
	props: ['energy_data']
};
</script>

<style scoped></style>
