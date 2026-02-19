<script lang="ts">
	import Tabs from '$lib/Tabs.svelte';
</script>

<main class="container">
	<Tabs
		list={[
			{ id: 'first', label: 'Menu Item' },
			{ id: 'second', label: 'Menu Item' }
		]}
	/>
	<div class="content-area"></div>
</main>

<style>
	:global(body) {
		display: flex;
		justify-content: center;
		align-items: center;
		background-color: #000000;
		padding: 40px;
		min-height: 100vh;
		font-family:
			-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;

		--container-bg: #e6ebf5;
		--tab-default: #6b6b6b;
		--tab-active: #2b75ed;
	}

	.container {
		display: flex;
		flex-direction: column;
		align-items: end;
		border: 1px solid #585a5e;
		border-radius: 32px;
		background-color: #07090e;
		width: 100%;
		max-width: 800px;
		max-height: 374px;
		overflow: hidden;
	}

	.content-area {
		display: flex;
		border-radius: 32px;
		background-color: var(--container-bg);
		width: 100%;
		min-height: 300px;
	}
</style>
