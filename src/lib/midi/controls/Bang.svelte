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
	import { msgKey, msgValue } from '../MIDIControls.svelte'

	export let key

	let bang, active

	$: if (key == $msgKey && $msgValue == 127) {
		active = true
		bang.click()
	} else {
		active = false
	}
</script>
