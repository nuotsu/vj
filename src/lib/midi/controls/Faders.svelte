{#each Object.entries(faders) as [legend, values]}
	<FaderSet {legend} {...values} />
{/each}

<script>
	import FaderSet from './FaderSet.svelte'
	import { writable } from 'svelte/store'

	const faders = {
		1: {
			k_key: 14,
			f_key: 3,
			t_key: 23, t: writable(false),
		},
		2: {
			k_key: 15,
			f_key: 4,
			t_key: 24, t: writable(false),
		},
		3: {
			k_key: 16,
			f_key: 5,
			t_key: 25, t: writable(false),
		},
		4: {
			k_key: 17,
			f_key: 6,
			t_key: 26, t: writable(false),
		},
		5: {
			k_key: 18,
			f_key: 7,
			t_key: 27, t: writable(false),
		},
		6: {
			k_key: 19,
			f_key: 8,
			t_key: 28, t: writable(false),
		},
		'7*': {
			k_key: 20,
			f_key: 9,
			t_key: 29, t: writable(false),
		},
		'8*': {
			k_key: 21,
			f_key: 10,
			t_key: 30, t: writable(false),
		},
		V: {
			k_key: 22,
			f_key: 11,
			t_key: 31, t: writable(false),
		},
	}
</script>
