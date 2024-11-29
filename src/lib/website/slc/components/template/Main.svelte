<script lang="ts">
	import type { Snippet } from 'svelte';
	let { children, sidebarRight }: { children?: Snippet; sidebarRight?: Snippet } = $props();
</script>

<main class:base={true} class:visible-right-sidebar={sidebarRight}>
	{@render children?.()}
	{@render sidebarRight?.()}
</main>

<style lang="postcss">
	.base {
		@apply grid grid-cols-1 space-y-4 bg-transparent p-4;
	}
	.visible-right-sidebar {
		@apply lg:grid-cols-[minmax(0px,1fr)_auto];
	}
</style>
