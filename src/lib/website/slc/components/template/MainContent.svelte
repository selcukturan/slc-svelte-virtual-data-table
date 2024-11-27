<script lang="ts">
	let { children } = $props();
</script>

<div class="rounded-sm border p-4">
	{@render children?.()}
</div>
