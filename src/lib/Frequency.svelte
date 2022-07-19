<div>
	{#each data as value}
		<output class="dynamic-color" style:--v={value / 255}>
			{value}
		</output>
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
