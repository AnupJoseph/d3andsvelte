<script>
	const data = [
		{ name: 'Group 1', value: 1 },
		{ name: 'Group 2', value: 2 },
		{ name: 'Group 3', value: 3 }
	];
	const fib = [0, 1, 2, 3, 5, 8];
</script>

<svg width="300" height="160">
	{#each data as grp, i}
		<g transform={`translate(${100 * i} 0)`}>
			{#each fib as f, j}
				<rect width={f * 10} height={f * 10} x="10" y="30" />
			{/each}
			<text x="10" y="10" dy="0.35em">{grp.name}</text>
		</g>
	{/each}
</svg>

<style>
	svg {
		border: 1px solid #ccc;
	}
	rect {
		stroke: chocolate;
		fill: transparent;
		stroke-width: 2;
	}
	text {
		font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial,
			sans-serif;
	}
</style>
