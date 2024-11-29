<script lang="ts">
	import '../app.postcss';
	import type { Snippet } from 'svelte';
	import { ModeWatcher } from 'mode-watcher';
	import { setGlobalContext } from '$lib/website/slc/contexts/global.svelte';
	import { afterNavigate } from '$app/navigation';
	import { Site, Header, Footer } from '$lib/website/slc/templates/base';
	let { children }: { children?: Snippet } = $props();

	const globalContext = setGlobalContext();

	afterNavigate(() => {
		globalContext.data.windowWidth = window.innerWidth;
	});

	$effect(() => {
		// CSS medya sorguları ile yapamadığımız şeyler için kullanılabilir JAVASCRIPT ekran ölçüleri
		const size = globalContext.data.screens;
		const w = globalContext.data.windowWidth;

		if (
			w === undefined ||
			size === undefined ||
			size.sm === undefined ||
			size.md === undefined ||
			size.lg === undefined
		) {
			return;
		}

		globalContext.data.currentScreen =
			w < size.sm
				? 'xs'
				: w >= size.sm && w < size.md
					? 'sm'
					: w >= size.md && w < size.lg
						? 'md'
						: 'lg';
	});
</script>

<svelte:window bind:innerWidth={globalContext.data.windowWidth} />

<ModeWatcher />

<Site>
	<Header />
	{@render children?.()}
	<Footer />
</Site>
