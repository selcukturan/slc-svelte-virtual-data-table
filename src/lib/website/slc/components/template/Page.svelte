<script lang="ts">
	let { children } = $props();
</script>

<div class="container mx-auto grid grid-cols-1 xl:grid-cols-[auto_minmax(0px,_1fr)]">
	{@render children?.()}
</div>
