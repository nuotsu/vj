<MIDISwitch/>
<SoundSwitch/>

{#if $midi}
	<MIDIControls/>
{/if}

{#if $sound}
	<AudioAnalyzer/>
	<Frequency/>
{/if}

<script>
	import MIDISwitch, { midi } from '$lib/MIDISwitch.svelte'
	import SoundSwitch, { sound } from '$lib/SoundSwitch.svelte'

	import MIDIControls from '$lib/MIDIControls.svelte'
	import AudioAnalyzer from '$lib/AudioAnalyzer.svelte'
	import Frequency from '$lib/Frequency.svelte'
</script>
