<button
	bind:this={bang}
	class:active
	on:click
>
	<slot></slot>
</button>

<style>
	button:active,
	.active {
		transform: scale(0.9);
	}
</style>

<script>
	import { messageKey, messageValue } from '../MIDIControls.svelte'

	export let key

	let bang, active

	$: if (key == $messageKey && $messageValue == 127) {
		active = true
		bang.click()
	} else {
		active = false
	}
</script>
