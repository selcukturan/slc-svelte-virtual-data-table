<script lang="ts">
	import '../app.postcss';
	import { ModeWatcher } from 'mode-watcher';
	import { setGlobalContext } from '$lib/website/slc/context/global.svelte';
	import { afterNavigate } from '$app/navigation';
	import { Site, Header, Footer, Page, Sidebar, Main } from '$lib/website/slc/components/template';

	let { children } = $props();

	const globalContext = setGlobalContext();

	afterNavigate(() => {
		globalContext.data.windowWidth = window.innerWidth;
	});

	$effect(() => {
		// CSS medya sorguları ile yapamadığımız şeyler için kullanılabilir ekran ölçüleri
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
	<Page>
		<Sidebar />
		<Main>
			{@render children?.()}
		</Main>
	</Page>
	<Footer>(footer)</Footer>
</Site>
