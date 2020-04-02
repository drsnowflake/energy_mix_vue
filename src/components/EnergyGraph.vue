<template>
	<g-chart
		type="PieChart"
		:options="chartOptions"
		:data="this.energy_data"
	></g-chart>
</template>

<script>
import { GChart } from 'vue-google-charts';

export default {
	name: 'energy-graph',
	data() {
		return {
			chartOptions: {
				is3D: true,
				backgroundColor: '#eeeeee'
			}
		};
	},

	props: ['energy_data'],
	components: {
		'g-chart': GChart
	}
};
</script>

<style scoped></style>
