<script>
	import { scaleLinear } from 'd3';

	const data = [0, 1, 2, 3, 4];
	const maxHeight = 140;

	let yScale = scaleLinear().domain([0, 4]).range([10, maxHeight]);
	let hueScale = scaleLinear().domain([0, 4]).range(['chartreuse', 'rgb(25, 44, 6)']);
</script>

<div />
<svg height="160" width="160">
	{#each data as i}
		<rect height={yScale(i)} width="20" y="10" x={10 + i * 30} fill={hueScale(i)} />
	{/each}
</svg>

<style>
	svg {
		border: 1px solid #ccc;
	}
</style>
