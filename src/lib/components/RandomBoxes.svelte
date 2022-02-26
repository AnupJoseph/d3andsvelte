<script>
	import { range, scaleOrdinal, schemeSet2 } from 'd3';

	const data = range(0, 150);
	const colors = scaleOrdinal().range(schemeSet2.slice(0, 6));
	console.log(colors);
</script>

<svg width="900" height="150">
	{#each data as d}
		{@const x = -30 + Math.random() * (900 + 30)}
		{@const y = -30 + Math.random() * (125 + 30)}
		<rect
			width="30"
			height="30"
			{x}
			{y}
			style={`fill:${colors(d)}`}
			transform={`rotate(${Math.random() * 90} ${x + 15} ${y + 15})`}
		/>
	{/each}
</svg>

<style>
	rect {
		opacity: 0.7;
		rx: 3;
	}
</style>
