<script lang="ts">
	import '../app.postcss';
	import { ModeWatcher } from 'mode-watcher';
	import Sun from 'lucide-svelte/icons/sun';
	import Moon from 'lucide-svelte/icons/moon';
	import { toggleMode } from 'mode-watcher';
	import { Button } from '$lib/website/components/ui/button';
	let { children } = $props();
</script>

<ModeWatcher />

<div class="grid grid-rows-[3.5rem_1fr_auto]">
	<!-- Header -->
	<header
		class="sticky top-0 z-50 h-[3.5rem] w-full border-b border-border/70 bg-background/95 backdrop-blur supports-[backdrop-filter]:bg-background/60"
	>
		(header)
	</header>
	<!-- Page -->
	<div class="container mx-auto grid grid-cols-1 xl:grid-cols-[auto_minmax(0px,_1fr)]">
		<!-- Sidebar (Left) -->
		<aside class="h-48 bg-transparent p-4 xl:sticky xl:top-[3.5rem] xl:h-screen xl:w-60">
			<div class="flex h-full w-full flex-col border border-border/70">
				<div class="hidden">h</div>
				<div class="flex flex-1 flex-col gap-2 overflow-hidden overflow-y-auto p-4">
					<div class="rounded-sm bg-amber-200 p-2 dark:bg-amber-700/20">test 1</div>
					<div class="rounded-sm bg-amber-200 p-2 dark:bg-amber-700/20">test 1</div>
					<div class="rounded-sm bg-amber-200 p-2 dark:bg-amber-700/20">test 1</div>
					<div class="rounded-sm bg-amber-200 p-2 dark:bg-amber-700/20">test 1</div>
					<div class="rounded-sm bg-amber-200 p-2 dark:bg-amber-700/20">test 1</div>
					<div class="rounded-sm bg-amber-200 p-2 dark:bg-amber-700/20">test 1</div>
					<div class="rounded-sm bg-amber-200 p-2 dark:bg-amber-700/20">test 1</div>
				</div>
				<div class="hidden">f</div>
			</div>
		</aside>

		<!-- Main -->
		<main class="space-y-4 bg-transparent p-4">
			<div class="h-[512px] rounded-sm border p-4">
				{@render children?.()}
			</div>
			<div class="h-[512px] rounded-sm border p-4">
				<Button onclick={toggleMode} variant="outline" size="icon">
					<Sun
						class="h-[1.2rem] w-[1.2rem] rotate-0 scale-100 transition-all dark:-rotate-90 dark:scale-0"
					/>
					<Moon
						class="absolute h-[1.2rem] w-[1.2rem] rotate-90 scale-0 transition-all dark:rotate-0 dark:scale-100"
					/>
					<span class="sr-only">Toggle theme</span>
				</Button>
			</div>
			<div class="h-[512px] rounded-sm border p-4">Paragraph 3</div>
		</main>
	</div>
	<!-- Footer -->
	<footer
		class="border-t border-border/70 bg-background/95 p-4 backdrop-blur supports-[backdrop-filter]:bg-background/60"
	>
		(footer)
	</footer>
</div>
