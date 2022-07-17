<label>
	<input type="checkbox" bind:checked>
</label>

<script>
	import { messageKey, messageValue } from '../MIDIControls.svelte'

	export let key

	let checked = false

	$: if (key === $messageKey && $messageValue === 127) {
		checked = !checked
	}
</script>
