<label>
	<input hidden type="checkbox" bind:checked={$checked}>
</label>

<script>
	import { messageKey, messageValue } from '../MIDIControls.svelte'

	export let key, checked

	$: if (key === $messageKey && $messageValue === 127) {
		$checked = !$checked
	}
</script>
