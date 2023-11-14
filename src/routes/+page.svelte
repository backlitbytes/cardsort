<script lang="ts">
	let laugh = $state(false);
</script>

Welcome to sveltekit{laugh ? ' LOL' : '!'}
<button
	onclick={() => {
		laugh = true;
	}}>Giggle time</button
>
