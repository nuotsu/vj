<button class:off={!$midi} on:click={() => $midi = !$midi}>
	🎛
</button>

<script context="module">
	import { writable } from 'svelte/store'

	export const midi = writable(false)
</script>
