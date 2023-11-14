<script lang="ts">
	// TypeScript script (if needed for more complex logic)
</script>

<main>
	<div class="card">
		<div class="card-inner">
			<div class="card-front" />
			<div class="card-back" />
		</div>
	</div>
</main>

<style>
	.card {
		width: 100px;
		height: 150px;
		perspective: 1000px;
	}

	.card-inner {
		width: 100%;
		height: 100%;
		position: relative;
		transform-style: preserve-3d;
		transition: transform 0.5s;
		animation: gamersRiseUp 10s ease-out forwards;
	}

	.card-front,
	.card-back {
		position: absolute;
		width: 100%;
		height: 100%;
		backface-visibility: hidden;
	}

	.card-front {
		background-color: black;
		background-image: url('/images/card-front.png');
		background-size: cover;
		background-position: center;
	}

	.card-back {
		background-color: red;
		transform: rotateY(180deg);
	}

	@keyframes gamersRiseUp {
		0% {
			transform: translateY(150px) rotateX(90deg);
		}
		100% {
			transform: translateY(0) rotateX(0deg);
		}
	}
</style>
