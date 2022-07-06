<SoundControl/>

{#if $sound}
	<AudioAnalyzer/>
	<Frequency/>
{/if}

<script>
	import SoundControl, { sound } from '$lib/SoundControl.svelte'
	import AudioAnalyzer from '$lib/AudioAnalyzer.svelte'
	import Frequency from '$lib/Frequency.svelte'
</script>
