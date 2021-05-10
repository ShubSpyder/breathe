<script>
	import BreathingCircle from '../components/BreathingCircle.svelte';

	const breathingCircleProps = {
		size: '16rem',
		durationHold: 4,
		durationInhale: 4,
		durationExhale: 4
	};
</script>

<div class="circle-container">
	<BreathingCircle {...breathingCircleProps} />
</div>

<style>
	@import '../styles/global.css';

	.circle-container {
		height: 70vh;
		width: 100vw;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}
</style>
