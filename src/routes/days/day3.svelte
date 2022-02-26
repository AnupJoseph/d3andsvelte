<script>
	import LearnAccessorWithCircle from '$lib/components/LearnAccessorWithCircle.svelte';

	import { max, mean } from 'd3';
	let data = [
		{ name: 'a', value: 1 },
		{ name: 'b', value: 2 },
		{ name: 'c', value: 3 },
		{ name: 'd', value: 5 },
		{ name: 'e', value: 8 }
	];
</script>

<p>
	Max = {max(data, (d) => d.value)}
</p>
<p>
	Mean = {mean(data, (d) => d.value)}
</p>
<p>
	Random Value = {max(data, (d) => d.value * Math.random())}
</p>

<LearnAccessorWithCircle {data} />
