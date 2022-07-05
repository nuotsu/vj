<button class:off={!$sound} on:click={() => $sound = !$sound}>
	🎧
</button>

<style>
	.off {
		opacity: 0.5;
	}
</style>

<script context="module">
	import { writable } from 'svelte/store'

	export const sound = writable(false)
</script>
