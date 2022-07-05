<SoundControl/>

{#if $sound}
	<AudioAnalyzer/>
{/if}

<h1>VJ</h1>

<script>
	import SoundControl, { sound } from '$lib/SoundControl.svelte'
	import AudioAnalyzer from '$lib/AudioAnalyzer.svelte'
</script>
