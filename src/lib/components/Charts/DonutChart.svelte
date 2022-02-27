<script>
	import { arc, pie, scaleOrdinal } from 'd3';

	const data = [
		{ type: 'Poultry', value: 48.9954 },
		{ type: 'Beef', value: 25.9887 },
		{ type: 'Pig', value: 22.9373 },
		{ type: 'Sheep', value: 0.4869 }
	];
	const height = 500,
		width = 900,
		colors = ['#976393', '#685489', '#43457f', '#ff9b83'];

	let colorScale = scaleOrdinal(
		data.map((d) => d.type),
		colors
	);
	let arcPath = arc()
		.innerRadius((0.5 * height) / 2)
		.outerRadius((0.85 * height) / 2);
	let piePath = pie().value((d) => d.value);
	let labelPath = arc()
		.innerRadius((0.95 * height) / 2)
		.outerRadius((0.95 * height) / 2);

	let pieArcs = piePath(data);
    console.log(pieArcs)
</script>

<svg {height} {width} >

</svg>

<style>
	svg {
		border: 1px solid #ccc;
	}
</style>
