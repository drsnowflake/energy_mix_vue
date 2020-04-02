<template>
	<div>
		<p v-for="mix in energy_data" v-bind:key="mix">
			{{ mix }}
		</p>
	</div>
</template>

<script>
import { GChart } from 'vue-google-charts';

export default {
	name: 'energy-graph',
	props: ['energy_data'],
	components: {
		GChart
	}
};
</script>

<style scoped></style>
