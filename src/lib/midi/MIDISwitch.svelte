<svelte:window on:keydown={onKeydown} />

<button class:off={!$midi} on:click={() => $midi = !$midi}>
	🎛
</button>

{#if $midi}
	<a href="https://addons.mozilla.org/firefox/downloads/file/3975194/fa003cbe5f5d4168b33f-1.0.xpi">
		Download Firefox Addon
	</a>
{/if}

<script context="module">
	import { writable } from 'svelte/store'

	export const midi = writable(false)

	function onKeydown({ key }) {
		if (key === '`') {
			midi.update(v => !v)
		}
	}
</script>
