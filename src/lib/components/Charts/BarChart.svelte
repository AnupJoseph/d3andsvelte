<script>
	import { axisBottom, axisLeft, max, scaleBand, scaleLinear, select } from 'd3';
	import { fly } from 'svelte/transition';

	const data = [
		{ year: 2005, value: 734.69 },
		{ year: 2006, value: 750.7 },
		{ year: 2007, value: 755.13 },
		{ year: 2008, value: 694.19 },
		{ year: 2009, value: 681.83 },
		{ year: 2010, value: 718.98 },
		{ year: 2011, value: 740.57 },
		{ year: 2012, value: 752.24 },
		{ year: 2013, value: 767.24 },
		{ year: 2014, value: 802.45 },
		{ year: 2015, value: 805.65 },
		{ year: 2016, value: 935.58 },
		{ year: 2017, value: 967.13 },
		{ year: 2018, value: 1007.24 }
	];
	const width = 900,
		height = 500,
		margin = { top: 10, right: 10, bottom: 25, left: 35 };

	const yMax = max(data, (d) => d.value);
	const xDomain = data.map((d) => d.year);

	let xScale = scaleBand()
		.domain(xDomain)
		.range([margin.left, width - margin.left - margin.right])
		.padding(0.5);
	let yScale = scaleLinear()
		.domain([0, yMax])
		.range([height - margin.bottom, margin.top]);

	let xg, yg, trans;

	let xAxis = axisBottom(xScale).tickSizeOuter(0);
	$: select(xg).call(xAxis);
	let yAxis = axisLeft(yScale).tickSizeOuter(0);
	$: select(yg).call(yAxis);
</script>

<!-- in:fly={{ y: -500, duration: 5000, delay: i * 15 }} -->
<svg {width} {height}>
	<g bind:this={xg} transform={`translate(0,${height - margin.bottom})`} />
	<g bind:this={yg} transform={`translate(${margin.left},0)`} />
	{#each data as d, i}
		<rect
			width={xScale.bandwidth()}
			height={yScale(0) - yScale(d.value)}
			x={xScale(d.year)}
			y={yScale(d.value)}
		/>
	{/each}
</svg>

<style>
	svg {
		border: 1px solid #ccc;
	}
	rect {
		fill: #7472c0;
	}
</style>
