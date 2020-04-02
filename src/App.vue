<template>
	<div>
		<h1>UK Energy sources</h1>
	</div>
</template>

<script>
export default {
	data() {
		return {
			energy_mix: {}
		};
	},
	mounted() {
		fetch('https://api.carbonintensity.org.uk/generation')
			.then(res => res.json())
			.then(json => (this.energy_mix = json))
			.then(console.log(this.energy_mix));
	}
};
</script>

<style scoped></style>
