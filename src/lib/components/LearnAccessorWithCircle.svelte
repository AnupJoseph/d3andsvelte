<script>
	export let data;
</script>

<svg width="160" height="160">
	{#each data as i}
		<circle cx={i.value * 10} cy="80" r={i.value * 10} fill="transparent" stroke="steelblue" />
		<text x={i.value * 20} y="80" dy="0.35em" text-anchor="end">{i.name}</text>
	{/each}
</svg>
