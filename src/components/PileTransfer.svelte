<script lang="ts">
  import { crossfade } from 'svelte/transition';
  import { quintOut } from 'svelte/easing';
  import { flip } from 'svelte/animate';

  const [send, receive] = crossfade({
    duration: (d) => Math.sqrt(d * 200),

    fallback(node, params) {
      const style = getComputedStyle(node);
      const transform = style.transform === 'none' ? '' : style.transform;

      return {
        duration: 600,
        easing: quintOut,
        css: (t) => `
          transform: ${transform} scale(${t});
          opacity: ${t}
        `
      };
    }
  });

	class Card {
		name = $state('');
		color = $state('');

		constructor(name: string, color: string) {
			this.name = name;
      this.color = color;
		}
	}

	let pile1 = $state([
		new Card('Card 1', 'grey'),
		new Card('Card 2', 'orange'),
		new Card('Card 3', 'blue')
	]);
	let pile2 = $state([
		new Card('Card 4', 'purple'),
		new Card('Card 5', 'green'),
		new Card('Card 6', 'eggshell')
	]);

	function moveCard(card: Card) {
		if (pile1.find((crd) => crd.name === card.name)) {
			pile1 = pile1.filter((c) => c !== card);
			pile2.push(card);
			pile2 = pile2;
		} else if (pile2.includes(card)) {
			pile2 = pile2.filter((c) => c !== card);
			pile1.push(card);
			pile1 = pile1;
		}
	}
</script>

{#snippet cardView(card)}
  <button class="card" on:click={() => moveCard(card)} style:background-color={card.color}
    in:receive={{ key: card.name }}
    out:send={{ key: card.name }}
    animate:flip={{ duration: 200 }}
  >
    {card.name}
  </button>
{/snippet}

<div class="piles">
	<div class="pile">
		{#each pile1 as card (card.name)}
      {@render cardView(card)}
		{/each}
	</div>

	<div class="pile">
		{#each pile2 as card (card.name)}
      {@render cardView(card)}
		{/each}
	</div>
</div>

<style>
	.pile {
		display: flex;
		gap: 10px;
		margin: 10px;
	}

	.card {
		width: 100px;
		height: 150px;
		border: 1px solid black;
		cursor: pointer;
	}
</style>
