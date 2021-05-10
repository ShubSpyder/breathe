<script>
	import { fly } from 'svelte/transition';

	// props I hope self explanatory
	export let size;
	export let durationHold;
	export let durationInhale;
	export let durationExhale;

	// console.log({ durationInhale }, { durationExhale });

	let changeDirection = false;
	let hold = false;

	function inhale() {
		changeDirection = !changeDirection;
		hold = false;
		setTimeout(() => {
			holdBreathe();
		}, durationHold * 1000);
	}

	function holdBreathe() {
		hold = true;
		setTimeout(() => {
			inhale();
		}, durationHold * 1000);
	}

	holdBreathe();
</script>

<div style="width:{size};height:{size}" class="container">
	<div class="outer-circle">
		<div
			class="inner-circle absolute"
			style="transition: {changeDirection
				? durationExhale
				: durationInhale}s; transform:scale({changeDirection ? 0.5 : 1})"
		/>
		{#if hold}
			<p in:fly={{ y: 10 }} out:fly={{ y: 10 }}>Hold</p>
		{:else}
			<p in:fly={{ y: -10 }} out:fly={{ y: -10 }}>{changeDirection ? 'Exhale' : 'Inhale'}</p>
		{/if}
	</div>
</div>

<style>
	@import '../styles/global.css';

	.container {
		@apply relative;
	}
	div {
		@apply rounded-full;
		@apply block;
	}
	.outer-circle {
		@apply items-center;
		@apply w-full;
		@apply justify-center;
		background: var(--outter-circle-bg);
		@apply h-full;
		@apply absolute;
		@apply transition;
		@apply flex;
		border: 1.2px solid var(--outter-circle-border);
	}
	.outer-circle > p {
		@apply absolute;
		@apply transition;
		color: #fff;
	}
	.inner-circle {
		width: 92%;
		height: 92%;
		border-radius: 50%;
		@apply absolute;
		background: var(--inner-circle-bg);
	}
</style>
