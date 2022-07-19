<fader style:--v={value / 127}>
	<indicator
		class:vertical
		style:--dir={vertical ? 'to top' : 'to right'}
	/>
	<output class="dynamic-color">{value}</output>
</fader>

<style>
	fader {
		display: flex;
		flex-direction: column;
		align-items: center;
		text-align: center;
	}

	indicator {
		display: block;
		block-size: 3px;
		inline-size: 100%;
		background-color: #fff2;
	}

	indicator::before {
		content: '';
		display: block;
		width: 100%;
		height: 100%;
		background-image: linear-gradient(var(--dir), currentColor, green);
		mask-image: linear-gradient(var(--dir), currentColor calc(var(--v) * 100%), transparent calc(var(--v) * 100%));
	}

	.vertical {
		writing-mode: vertical-lr;
		max-inline-size: 100px;
	}
</style>

<script>
	import { messageKey, messageValue } from '../MIDIControls.svelte'

	export let key, vertical

	let value = 0

	$: if (key === $messageKey) {
		value = $messageValue
	}
</script>
