<label>
	<input type="hidden" bind:value {max} />

	<knob style:--v={value / max}>
		<indicator/>
		<output>{value}</output>
	</knob>

	<slot></slot>
</label>

<style>
	knob {
		display: grid;
		width: 3em;
		border-radius: 100%;
		overflow: hidden;
	}

	indicator {
		grid-column: 1 / -1;
		grid-row: 1 / -1;
		transform: rotate(-135deg);
		display: grid;
		aspect-ratio: 1;
		width: 100%;
		mask-image: radial-gradient(circle, transparent 64%, currentColor 64%);
	}

	indicator::before {
		content: '';
		grid-column: 1 / -1;
		grid-row: 1 / -1;
		display: block;
		aspect-ratio: 1;
		width: 100%;
		border-radius: 100%;
		background-color: #fff2;
		mask-image: conic-gradient(currentColor 0.75turn, transparent 0.75turn);
	}

	indicator::after {
		content: '';
		grid-column: 1 / -1;
		grid-row: 1 / -1;
		display: block;
		aspect-ratio: 1;
		width: 100%;
		background-image: conic-gradient(currentColor, green 0.75turn, transparent 0.75turn);
		mask-image: conic-gradient(currentColor calc(var(--v) * 0.75turn), transparent calc(var(--v) * 0.75turn));
	}

	output {
		grid-column: 1 / -1;
		grid-row: 1 / -1;
		display: grid;
		place-content: center;
		color: hsla(120, 100%, calc(100% - var(--v) * 50%));
	}
</style>

<script>
	import { messageKey, messageValue } from '../MIDIControls.svelte'

	export let key

	let value = 0, max = 127

	$: if (key === $messageKey) {
		value = $messageValue
	}
</script>
