<script lang="ts">
	import type { Snippet } from 'svelte';
	let { children }: { children?: Snippet } = $props();
</script>

<div class="rounded-sm border p-4">
	{@render children?.()}
</div>
