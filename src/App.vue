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
			energy_mix: [],
			graph_mix: []
		};
	},
	// computed: {
	// 	convertData() {
	// 		console.log(this.energy_mix);
	// 	}
	// },
	mounted() {
		fetch('https://api.carbonintensity.org.uk/generation')
			.then(res => res.json())
			// .then(json =>
			// 	json.data.generationmix.forEach(d => this.energy_mix.push(d))
			.then(data => this.convertData(data));
	},
	methods: {
		convertData: function(data) {
			console.log(data.data.generationmix);
			data.forEach(data => this.energy_mix.push(data.data.generationmix.fuel));
		}
	},
	components: {
		'energy-graph': EnergyGraph
	}
};
</script>

<style scoped></style>
