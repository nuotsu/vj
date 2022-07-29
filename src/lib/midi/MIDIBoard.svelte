<details class="glass" open={$board}>
	<summary on:click={() => $board = !$board}>🎛</summary>

	<div>
		<slot></slot>
	</div>
</details>

<style>
	details {
		position: fixed;
		inset: auto 0 0;
	}

	details[open] {
		border-top: 1px solid;
	}

	details:not([open]) {
		right: auto;
	}

	details:not([open]) summary {
		@apply off;
	}

	details[open] summary {
		position: absolute;
		left: 0;
		top: 0;
		margin: 0.5rem;
	}

	details[open] div {
		animation: open 0.2s ease-in-out forwards;
	}

	@keyframes open {
		from {
			opacity: 0;
			transform: translateY(2rem);
		}
	}
</style>

<script context="module">
	import { writable } from 'svelte/store'

	export const board = writable(true)
</script>
