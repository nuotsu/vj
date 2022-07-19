<nav>
	<fieldset>
		<div class="flex items-center gap-2">
			<Bang key={67} on:click={() => console.log('⬅️')}>⬅️</Bang>
			<Knob key={10} />
			<Bang key={64} on:click={() => console.log('➡️')}>➡️</Bang>
		</div>

		<Fader key={9} />
	</fieldset>

	<Faders/>

	<fieldset>
		<Bang key={1} on:click={() => console.log('1️⃣')}>1️⃣</Bang>
		<Bang key={2} on:click={() => console.log('2️⃣')}>2️⃣</Bang>

		<Bang key={49} on:click={() => console.log('🔄')}>🔄</Bang>
		<Bang key={47} on:click={() => console.log('⏪')}>⏪</Bang>
		<Bang key={48} on:click={() => console.log('⏩')}>⏩</Bang>
		<Bang key={46} on:click={() => $sound = false}>⏹</Bang>
		<Bang key={45} on:click={() => $sound = true}>▶️</Bang>
		<Bang key={44} on:click={() => console.log('⏺')}>⏺</Bang>
	</fieldset>
</nav>

<style>
	fieldset {
		border: 1px solid;
	}
</style>

<script>
	import Knob from './inputs/Knob.svelte'
	import Fader from './inputs/Fader.svelte'
	import Bang from './inputs/Bang.svelte'

	import { sound } from '$lib/SoundSwitch.svelte'
	import Faders from './controls/Faders.svelte'

	export let input

	input.onmidimessage = ({ data }) => {
		let [_, key, value] = data
		console.log(key, value)
		$messageKey = key
		$messageValue = value
	}

	input.onstatechange = ({ target }) => {
		console.info(`${target.name}: ${target.state}`)
	}
</script>

<script context="module">
	import { writable } from 'svelte/store'

	export const messageKey = writable(null)
	export const messageValue = writable(null)

	export async function requestMIDI() {
		if ('navigator' in window) {
			let midiAccess = await navigator.requestMIDIAccess()
			let [input] = midiAccess.inputs.values()
			return input
		}
	}
</script>
