<template>
	<div>
		<h1>UK Energy sources</h1>
		<energy-graph :energy_data="energy_mix"></energy-graph>
	</div>
</template>

<script>
import EnergyGraph from './components/EnergyGraph';

export default {
	data() {
		return {
			energy_mix: {},
			graph_mix: []
		};
	},
	mounted() {
		fetch('https://api.carbonintensity.org.uk/generation')
			.then(res => res.json())
			.then(json => (this.energy_mix = json.data.generationmix))
			.then(console.log('starting loop'))
			.then(convertData())
			.then(console.log('finishing loop'));
	},
	components: {
		'energy-graph': EnergyGraph
	},
	methods: {
		convertData: function() {
			this.energy_mix.forEach(d => console.log(d));
		}
	}
};
</script>

<style scoped></style>
