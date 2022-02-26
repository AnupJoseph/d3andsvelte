<script>
	import { range, scaleLinear, schemeRdYlBu } from 'd3';

	const data = range(0, 8);
	const fib = [0, 1, 2, 3, 5, 8, 13].reverse();
	const colors = scaleLinear().domain(data).range(schemeRdYlBu[6]);
	console.log(colors);
</script>

<svg width="780" height="130">
	{#each data as d, i}
		<g transform={`translate(${130 * i},0)`}>
			{#each fib as f, j}
				{@const prop = f * 10}
				{@const position = 65 - f * 5}
				<rect x={position} y={position} width={prop} height={prop} style={`fill:${colors(j)}`} />
			{/each}
		</g>
	{/each}
</svg>

<style>
	svg {
		border: 1px solid #ccc;
	}
</style>
