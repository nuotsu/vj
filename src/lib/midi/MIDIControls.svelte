<nav>
	<section style="grid-area: main">
		<fieldset class="flex items-center justify-center gap-2">
			<Bang key={67} on:click={() => console.log('⬅️')}>⬅️</Bang>
			<Knob key={10} />
			<Bang key={64} on:click={() => console.log('➡️')}>➡️</Bang>
		</fieldset>

		<Fader key={9} />
	</section>

	<section style="grid-area: faders">
		{#each Object.entries(faders) as [legend, values]}
			<FaderSet {legend} {...values} />
		{/each}
	</section>

	<section class="bottom">
		<fieldset>
			<Bang key={1} on:click={() => console.log('1️⃣')}>1️⃣</Bang>
			<Bang key={2} on:click={() => console.log('2️⃣')}>2️⃣</Bang>
		</fieldset>
		<fieldset>
			<Bang key={49} on:click={() => console.log('🔄')}>🔄</Bang>
			<Bang key={47} on:click={() => console.log('⏪')}>⏪</Bang>
			<Bang key={48} on:click={() => console.log('⏩')}>⏩</Bang>
			<Bang key={46} on:click={() => $sound = false}>⏹</Bang>
			<Bang key={45} on:click={() => $sound = true}>▶️</Bang>
			<Bang key={44} on:click={() => console.log('⏺')}>⏺</Bang>
		</fieldset>
	</section>
</nav>

<style>
	nav {
		display: grid;
		grid-template-areas:
			'main faders'
			'bottom bottom';
		grid-template-columns: auto 1fr;
	}

	.bottom {
		grid-area: bottom;
		display: grid;
		grid-template-columns: 1fr auto;
		align-items: center;
		gap: 1rem;
	}
</style>

<script>
	import Knob from './inputs/Knob.svelte'
	import Fader from './inputs/Fader.svelte'
	import Bang from './inputs/Bang.svelte'

	import { sound } from '$lib/SoundSwitch.svelte'
	import faders from './controls/faders'
	import FaderSet from './controls/FaderSet.svelte'

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
