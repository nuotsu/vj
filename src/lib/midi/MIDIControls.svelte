<nav>
	<fieldset>
		<Bang key={67} on:click={() => console.log('🫲')}>🫲</Bang>
		<Knob key={10} />
		<Bang key={64} on:click={() => console.log('🫱')}>🫱</Bang>

		<Fader key={9} />

		<Bang key={1} on:click={() => console.log('1️⃣')}>1️⃣</Bang>
		<Bang key={2} on:click={() => console.log('2️⃣')}>2️⃣</Bang>
	</fieldset>

	{#each Object.entries(faders) as [legend, [knob, fader, toggle]]}
		<fieldset>
			<legend>{legend}</legend>
			<Knob key={knob} />
			<Fader key={fader} />
			<Toggle key={toggle} />
		</fieldset>
	{/each}

	<fieldset>
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
	import Knob from './controls/Knob.svelte'
	import Fader from './controls/Fader.svelte'
	import Bang from './controls/Bang.svelte'
	import Toggle from './controls/Toggle.svelte'

	import faders from './controls/faders'
	import { sound } from '$lib/SoundSwitch.svelte'

	export let input

	input.onmidimessage = e => {
		let [_, key, value] = e.data
		console.log(e)
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
