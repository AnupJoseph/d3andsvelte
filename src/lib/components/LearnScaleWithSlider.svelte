<script>
	import { scaleLinear, scaleOrdinal } from 'd3';

	let xSliderValue = 3,
		ySliderValue = 45,
		colorValue = 'steelblue';
	$: xScale = scaleOrdinal().domain([0, 1, 2, 3, 4]).range([0, 30, 60, 90, 140]);
	$: yScale = scaleLinear().domain([0, 140]).range([10, 130]);
	$: colorScale = scaleLinear().domain([0, 100]).range(['#eee', 'steelblue']);
</script>

<svg width="160" height="160">
	<rect
		width="20"
		height="20"
		x={xScale(xSliderValue)}
		y={yScale(ySliderValue)}
		style={`fill: ${colorScale(colorValue)};`}
	/>
</svg>

<div />
<input type="range" name="XRange" id="xrange" bind:value={xSliderValue} min="0" max="4" />
<div />
<input type="range" name="YRange" id="yrange" bind:value={ySliderValue} min="0" max="140" />
<div />
<input type="range" name="ColorRange" id="color-range" bind:value={colorValue} min="0" max="100" />

<style>
	svg {
		border: 1px solid #cdcdcd;
	}
</style>
