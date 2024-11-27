<script lang="ts">
	let { children } = $props();
</script>

<header
	class="border-t border-border/70 bg-background/95 p-4 backdrop-blur supports-[backdrop-filter]:bg-background/60"
>
	{@render children?.()}
</header>
