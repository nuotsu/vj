<button class:off={!$sound} on:click={() => $sound = !$sound}>
	🎧
</button>

<script context="module">
	import { writable } from 'svelte/store'

	export const sound = writable(false)
</script>
