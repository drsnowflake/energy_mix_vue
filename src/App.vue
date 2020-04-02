<template>
	<div>
		<h1>UK Energy sources</h1>
		<energy-graph id="pie-chart" :energy_data="generationMix"></energy-graph>
	</div>
</template>

<script>
import EnergyGraph from './components/EnergyGraph';

export default {
	data() {
		return {
			generationMix: []
		};
	},
	mounted() {
		fetch('https://api.carbonintensity.org.uk/generation')
			.then(res => res.json())
			.then(json => this.convertData(json));
	},
	methods: {
		convertData: function(json) {
			// console.log(json.data.generationmix);
			this.generationMix.push(['Fuel', 'Percentage']);
			json.data.generationmix.forEach(d =>
				this.generationMix.push([d.fuel, d.perc])
			);
		}
	},
	components: {
		'energy-graph': EnergyGraph
	}
};
</script>

<style scoped>
#pie-chart {
	height: 30em;
	width: max;
}
</style>
