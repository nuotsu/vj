<MIDISwitch/>
<SoundSwitch/>

{#if $midi}
	{#await requestMIDI() then input}
		<MIDIControls {input} />
	{/await}
{/if}

{#if $sound}
	<AudioAnalyzer/>
	<Frequency/>
{/if}

<script>
	import MIDISwitch, { midi } from '$lib/midi/MIDISwitch.svelte'
	import SoundSwitch, { sound } from '$lib/SoundSwitch.svelte'

	import MIDIControls, { requestMIDI } from '$lib/midi/MIDIControls.svelte'
	import AudioAnalyzer from '$lib/AudioAnalyzer.svelte'
	import Frequency from '$lib/Frequency.svelte'
</script>
