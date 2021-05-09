<script>
	import BreathingCircle from '../components/BreathingCircle.svelte';
	// examples of breathingCircle Component
	const breathingCircleProps = {
		size: '300px',
		durationBreathe: 3,
		durationHold: 2
	};
	const breathingCircleProps2 = {
		size: '200px',
		durationBreathe: 2,
		durationHold: 3
	};
</script>

<BreathingCircle {...breathingCircleProps} />
<BreathingCircle {...breathingCircleProps2} />
