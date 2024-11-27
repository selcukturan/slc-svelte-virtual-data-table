<script lang="ts">
	import type { Snippet } from 'svelte';
	let { children }: { children?: Snippet } = $props();
</script>

<main class="space-y-4 bg-transparent p-4">
	{@render children?.()}
</main>
