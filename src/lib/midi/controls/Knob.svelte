<label>
	<slot></slot>

	<input type="hidden"
		bind:value min={0} max={127}
	/>

	<meter {value} min={0} max={127} />
</label>

<script>
	import { messageKey, messageValue } from '../MIDIControls.svelte'

	export let key

	let value = 0

	$: if (key === $messageKey) {
		value = $messageValue
	}
</script>
