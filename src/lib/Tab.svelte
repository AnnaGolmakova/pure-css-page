<script lang="ts">
	import { animate } from 'motion';

	interface Props {
		isActive: boolean;
		label: string;
		onclick?: () => void;
	}

	let { isActive, label, onclick }: Props = $props();

	let svgElement: SVGSVGElement | undefined = $state();

	const bounce = {
		duration: 0.6,
		ease: bounceEase
	};

	const spring = {
		type: 'spring',
		stiffness: 700,
		damping: 30
	};

	// From https://easings.net/#easeOutBounce
	function bounceEase(x: number) {
		const n1 = 7.5625;
		const d1 = 2.75;

		if (x < 1 / d1) {
			return n1 * x * x;
		} else if (x < 2 / d1) {
			return n1 * (x -= 1.5 / d1) * x + 0.75;
		} else if (x < 2.5 / d1) {
			return n1 * (x -= 2.25 / d1) * x + 0.9375;
		} else {
			return n1 * (x -= 2.625 / d1) * x + 0.984375;
		}
	}

	$effect(() => {
		if (svgElement) {
			const targetHeight = isActive ? 16 : 0;
			const transition = isActive ? bounce : spring;

			animate(svgElement, { height: targetHeight }, transition);
		}
	});
</script>

<button
	class={[isActive && 'active', 'tab']}
	type="button"
	role="tab"
	aria-selected={isActive}
	tabindex={isActive ? 0 : -1}
	{onclick}
>
	{label}
	<svg
		bind:this={svgElement}
		class="indicator"
		width="87"
		height={isActive ? 16 : 0}
		viewBox="0 0 87 16"
		fill="none"
		xmlns="http://www.w3.org/2000/svg"
	>
		<path
			d="M43.9242 0.000965479C61.584 0.136281 66.9243 13.9992 86.9243 13.9992V16.0001H43.4242L0 16L9.24021e-05 13.9992C18.0001 13.9992 26.2644 -0.13435 43.9242 0.000965479Z"
			fill="currentColor"
		/>
	</svg>
</button>

<style>
	.tab {
		display: flex;
		position: relative;
		justify-content: center;
		align-items: center;
		cursor: pointer;
		border: none;
		background-color: transparent;
		padding: 0 24px;
		height: 100%;
		color: var(--tab-default);
		font-weight: 400;
		font-size: 20px;
		letter-spacing: 0.3px;
	}

	.active {
		cursor: unset;
		color: var(--tab-active);
	}

	.indicator {
		position: absolute;
		bottom: -2px;
		margin: auto;
		color: var(--container-bg);
	}
</style>
