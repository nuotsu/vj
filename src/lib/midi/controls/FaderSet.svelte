<fieldset
	class="flex items-center gap-2"
	style:border-color={$t ? 'green' : 'currentColor'}
>
	<legend>{legend}</legend>

	<Knob key={k_key} />
	<Fader key={f_key} />
	<Toggle key={t_key} checked={t} />
</fieldset>

<style>
	fieldset {
		border: 1px solid;
	}
</style>

<script>
	import Knob from '../inputs/Knob.svelte'
	import Fader from '../inputs/Fader.svelte'
	import Toggle from '../inputs/Toggle.svelte'

	export let legend,
		k_key,
		f_key,
		t_key, t
</script>
