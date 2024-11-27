<script lang="ts">
	let { children } = $props();
	/* Header height'i değiştirmek için `Sidebar` ve ``Header`da değişiklik yapılacak */
	/* Header Height = 3.5rem = grid-rows-[3.5rem_1fr_auto] */
</script>

<div class="grid grid-rows-[3.5rem_1fr_auto]">
	{@render children?.()}
</div>
