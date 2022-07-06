<div>
	{#each data as d}
	<output>{d}</output>
	{/each}
</div>

<style>
	div {
		display: grid;
		grid-template-columns: repeat(32, 1fr);
		text-align: right;
	}

	output {
		display: block;
	}
</style>

<script>
	import { onMount } from 'svelte'
	import { analyzer } from './AudioAnalyzer.svelte'

	let frame, data = []

	function loop() {
		frame = requestAnimationFrame(loop)

		if (!$analyzer) return

		const dataArray = new Uint8Array($analyzer.frequencyBinCount)
		$analyzer.getByteFrequencyData(dataArray)

		data = Array.from(dataArray)
	}

	onMount(() => {
		loop()

		return () => cancelAnimationFrame(frame)
	})
</script>
