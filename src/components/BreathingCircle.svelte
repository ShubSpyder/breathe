<script>
	import { fly } from 'svelte/transition';

	// props I hope self explanatory
	export let size = '200px';
	export let durationBreathe = 3;
	export let durationHold = 2;

	let changeDirection = false;
	let hold = false;

	function inhale() {
		changeDirection = !changeDirection;
		hold = false;
		setTimeout(() => {
			holdBreathe();
		}, durationBreathe * 1000);
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
			style="transition: {durationBreathe}s; transform:scale({changeDirection ? 0.5 : 1})"
		/>
		{#if hold}
			<p in:fly={{ y: 10 }} out:fly={{ y: 10 }}>Hold</p>
		{/if}
		{#if !hold}
			<p in:fly={{ y: -10 }} out:fly={{ y: -10 }}>{changeDirection ? 'Inhale' : 'Exhale'}</p>
		{/if}
	</div>
</div>

<style>
	.container {
		@apply relative;
	}
	div {
		@apply rounded-full block;
	}
	.outer-circle {
		@apply items-center w-full justify-center h-full absolute bg-blue-100 transition flex;
	}
	.outer-circle > p {
		@apply absolute transition;
	}
	.inner-circle {
		@apply w-full h-full absolute bg-blue-200;
	}
</style>
