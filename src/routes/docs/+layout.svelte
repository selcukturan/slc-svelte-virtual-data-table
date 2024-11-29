<script lang="ts">
	import type { Snippet } from 'svelte';
	import { Page, Main, SidebarLeft, SidebarRight } from '$lib/website/slc/components/template';
	let { children }: { children?: Snippet } = $props();
</script>

<Page>
	{#snippet sidebarLeft()}
		<SidebarLeft />
	{/snippet}

	{@render children?.()}
</Page>
