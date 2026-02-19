<script lang="ts">
	import Tab from '$lib/Tab.svelte';

	interface Props {
		list: { id: string; label: string }[];
	}

	let { list }: Props = $props();

	let active = $state(list.length ? list[0].id : '');

	function setSelectedTab(id: string) {
		active = id;
	}

	function selectNext() {
		const currentIndex = list.findIndex((item) => item.id === active);
		const nextIndex = (currentIndex + 1) % list.length;
		active = list[nextIndex].id;
	}

	function selectPrev() {
		const currentIndex = list.findIndex((item) => item.id === active);
		const prevIndex = currentIndex === 0 ? list.length - 1 : currentIndex - 1;
		active = list[prevIndex].id;
	}

	function selectFirst() {
		if (list.length > 0) {
			active = list[0].id;
		}
	}

	function selectLast() {
		if (list.length > 0) {
			active = list[list.length - 1].id;
		}
	}

	function handleKeydown(event: KeyboardEvent) {
		switch (event.key) {
			case 'ArrowRight':
			case 'ArrowDown':
				event.preventDefault();
				selectNext();
				break;
			case 'ArrowLeft':
			case 'ArrowUp':
				event.preventDefault();
				selectPrev();
				break;
			case 'Home':
				event.preventDefault();
				selectFirst();
				break;
			case 'End':
				event.preventDefault();
				selectLast();
				break;
		}
	}
</script>

<div class="menu" role="tablist" onkeydown={handleKeydown}>
	{#each list as item (item.id)}
		<Tab label={item.label} isActive={item.id === active} onclick={() => setSelectedTab(item.id)} />
	{/each}
</div>

<style>
	.menu {
		display: flex;
		flex-direction: row;
		align-items: center;
		padding: 0 28px;
		height: 90px;
	}
</style>
