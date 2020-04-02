<template>
	<body>
		<div>
			<h1>UK Energy sources</h1>
			<energy-graph id="pie-chart" :energy_data="generationMix"></energy-graph>
		</div>
		<form v-on:submit.prevent>
			<label for="date_from">Date From:</label>
			<input id="date_from" type="datetime-local" v-model="dateFrom" />
			-------
			<label for="date_to">Date to:</label>
			<input id="date_to" type="datetime-local" v-model="dateTo" />

			<button v-on:click="updateChart">Submit</button>
		</form>
	</body>
</template>

<script>
import EnergyGraph from './components/EnergyGraph';

export default {
	data() {
		return {
			generationMix: [],
			dateFrom: null,
			dateTo: null
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
		},
		updateChart: function() {
			console.log('From', this.dateFrom);
			console.log('To', this.dateTo);
		}
	},
	components: {
		'energy-graph': EnergyGraph
	}
};
</script>

<style scoped>
body {
	font-family: 'Trebuchet MS', sans-serif;
	background-color: #ffe4c4;
	background-size: cover;
	text-align: center;
}

#pie-chart {
	height: 30em;
	width: max;
}

input[type='datetime-local'] {
	font-family: 'Trebuchet MS', sans-serif;
	padding: 10px;
}

button {
	background-color: #4caf50;
	border: none;
	color: white;
	padding: 10px 28px;
	text-align: center;
	text-decoration: none;
	display: inline-block;
	font-size: 14px;
	margin: 10px;
	cursor: pointer;
	-webkit-transition-duration: 0.4s;
	transition-duration: 0.4s;
}

button:hover {
	box-shadow: 0 12px 16px 0 rgba(0, 0, 0, 0.24),
		0 17px 50px 0 rgba(0, 0, 0, 0.19);
}
</style>
