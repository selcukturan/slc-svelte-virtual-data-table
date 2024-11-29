<script lang="ts">
	import type { Snippet } from 'svelte';
	let { children }: { children?: Snippet } = $props();
</script>

<!-- Header height'i değiştirmek için `SidebarLeft`, `SidebarRight` ve ``Header`da değişiklik yapılacak -->
<!-- Header Height = 3.5rem = grid-rows-[3.5rem_1fr_auto] -->
<div class="grid grid-rows-[3.5rem_1fr_auto]">
	{@render children?.()}
</div>
