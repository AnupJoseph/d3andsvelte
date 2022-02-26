<script>
	// export const ssr = false;
	import { select } from 'd3';

	const data = [0, 1, 2, 3, 4];
</script>

<svg width="40" height="40">
	<rect height="20" width="20" x="10" y="10" />
</svg>
<div />
<svg height="40" width="160">
	{#each data as i}
		<rect height="20" width="20" y="10" x={10 + i * 30} />
	{/each}
</svg>

<style>
	svg {
		border: 1px solid #ccc;
	}
	rect {
		fill: chartreuse;
	}
</style>
