<script lang="ts">
	import Card from '../components/Card.svelte';
	import PileTransfer from '../components/PileTransfer.svelte';

	let laugh = $state(false);
</script>

Welcome to sveltekit{laugh ? ' LOL' : '!'}
<button
	onclick={() => {
		laugh = true;
	}}>Giggle time</button
>

<Card />
<PileTransfer />
