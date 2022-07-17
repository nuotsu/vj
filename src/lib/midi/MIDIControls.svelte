<nav>
	<Bang key={46} on:click={() => $sound = false}>⏹</Bang>
	<Bang key={45} on:click={() => $sound = true}>▶️</Bang>
</nav>

<script>
	import Bang from './controls/Bang.svelte'

	import { sound } from '$lib/SoundSwitch.svelte'

	export let input

	input.onmidimessage = ({ data }) => {
		let [_, key, value] = data
		console.log(key, value)
		$msgKey = key
		$msgValue = value
	}

	input.onstatechange = ({ target }) => {
		console.info(`${target.name}: ${target.state}`)
	}
</script>

<script context="module">
	import { writable } from 'svelte/store'

	export const msgKey = writable(null)
	export const msgValue = writable(null)

	export async function requestMIDI() {
		if ('navigator' in window) {
			let midiAccess = await navigator.requestMIDIAccess()
			let [input] = midiAccess.inputs.values()
			return input
		}
	}
</script>
