{#await requestMIDI()}
	<!-- {console.log($device)} -->
{:catch error}
	{console.log(error)}
{/await}

<script>
	async function requestMIDI() {
		if ('navigator' in window) {
			let midiAccess = await navigator.requestMIDIAccess()

			midiAccess.inputs.forEach(entry => {
				entry.onmidimessage = event => {
					var str = "MIDI message received at timestamp " + event.timeStamp + "[" + event.data.length + " bytes]: ";
					for (var i=0; i<event.data.length; i++) {
						str += "0x" + event.data[i].toString(16) + " ";
					}
					console.log(str);
				}

				entry.onstatechange = e => {
					console.log(e)
				}
			})

			for (var output of midiAccess.outputs) {
				console.log({output})
			}
		}
	}
</script>

<script context="module">
	import { writable } from 'svelte/store'

	export const device = writable(null)
</script>
