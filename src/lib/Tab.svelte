<script lang="ts">
	interface Props {
		isActive: boolean;
		label: string;
		onclick?: () => void;
	}

	let { isActive, label, onclick }: Props = $props();
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
</style>
