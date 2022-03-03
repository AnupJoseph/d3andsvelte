<script>
	import {
		axisBottom,
		axisLeft,
		csv,
		curveNatural,
		format,
		line,
		max,
		scaleLinear,
		scaleOrdinal,
		scaleTime,
		schemeCategory10
	} from 'd3';
	import { onMount } from 'svelte';

	// Loading dataset
	let dataset = [];
	const row = (data) => {
		const date = new Date(data.date);
		const price = +data.dollar_price;
		return { iso: data.iso_a3, date: date, price: price, name: data.name };
	};
	onMount(async () => {
		dataset = await csv(`../data/big-mac-raw-index@1.csv`, row).then((data) => {
			return [
				data.filter(({ iso }) => iso === 'USA'),
				data.filter(({ iso }) => iso === 'SWE'),
				data.filter(({ iso }) => iso === 'CHN'),
				data.filter(({ iso }) => iso === 'EUZ')
			];
		});
	});

	// Data visualization
	const width = 900,
		height = 500,
		margin = { top: 10, right: 80, bottom: 30, left: 35 };

	const countryNames = dataset.map((d) => d[0].name);
	let colorScale = scaleOrdinal(countryNames, schemeCategory10);

	console.log(dataset[0]);
	const startDate = dataset?.[0]?.[0].date,
		endDate = dataset?.[0]?.[dataset[0]?.length - 1].date;
	let xScale = scaleTime([startDate, endDate], [margin.left, width - margin.right]);

	const prices = dataset.flat().map((d) => d.price),
		yMax = max([...prices, 8]);
	let yScale = scaleLinear([1, yMax], [height - margin.bottom, margin.top]);

	const formatter = format('$.2f');
	let xAxis = axisLeft(xScale).tickFormat((d) => formatter(d));

	let yAxis = axisBottom(yScale);

	$: lineGenerator = [];
	for (let index = 0; index < dataset?.length; index++) {
		const element = dataset?.[index];
		lineGenerator.append(
			line()
				.x((d) => xScale(d.date))
				.y((d) => yScale(d.price))
				.curve(curveNatural)(element)
		);
	}
</script>

<svg {width} {height}>
	{#each dataset as data, i}
		<path d={lineGenerator[i]} />
	{/each}
</svg>

<style>
	svg {
		border: 1px solid #ccc;
	}
	path {
		stroke-width: 2;
		fill: transparent;
	}
</style>
