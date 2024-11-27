<script lang="ts" generics="TData extends Row">
	import type { Row, Footers } from './types';
	import type { HTMLAttributes } from 'svelte/elements';
	import type { Snippet } from 'svelte';
	import { tick } from 'svelte';
	import { getTable } from './tables.svelte';

	type Props = HTMLAttributes<HTMLDivElement> & {
		data?: TData[];
		toolbar?: Snippet;
		thead?: Snippet;
		tbody?: Snippet<[TData, number]>;
		tfoot?: Snippet<[Footers<TData>, number]>;
		statusbar?: Snippet;
		class?: string;
		tableContainerClass?: string;
		containerClass?: string;
		height?: string;
		width?: string;
	};
	const {
		data,
		toolbar,
		thead,
		tbody,
		tfoot,
		statusbar,
		class: tableClass,
		tableContainerClass,
		containerClass,
		height = '100%',
		width = '100%',
		...attributes
	}: Props = $props();

	const table = getTable<TData>();

	const scrollAction = (tableNode: HTMLDivElement) => {
		let isScrolling: boolean = false;

		const setScrollTop = async () => {
			if (isScrolling) return; // Eğer fonksiyon zaten çalışıyorsa, yeni çağrıyı atlar
			const { scrollLeft, scrollTop, clientHeight, clientWidth, scrollHeight, scrollWidth } =
				tableNode;
			if (scrollTop === table.lastScrollTop) return; // virtual scroll özelliği sadece dikey scroll'da çalışır

			table.lastScrollTop = scrollTop;
			isScrolling = true;

			const scrollableHeight = scrollHeight - clientHeight;
			const scrollableWidth = scrollWidth - clientWidth;
			const scrollableTop = Math.floor(scrollTop);
			const scrollableLeft = Math.floor(scrollLeft);

			table.scrollTop = scrollTop; // scrollTop değiştiğinde `data` yeniden hesaplanır
			await tick(); // table.scrollTop state'i değiştiğinde, dom'da yapılacak tüm değişiklikleri bekler.

			// iOS cihazlardaki bounce effect kontrolü.
			// Scroll yapılabilir alanın dışına çıkıldığında `tableNode.scrollTo` manuel çalıştırılmaz.
			if (
				scrollableTop >= 0 &&
				scrollableTop <= scrollableHeight &&
				scrollableLeft >= 0 &&
				scrollableLeft <= scrollableWidth
			) {
				tableNode.scrollTo({ top: table.scrollTop });
			}

			isScrolling = false;
		};

		tableNode.addEventListener('scroll', setScrollTop, { passive: true });

		return {
			destroy() {
				tableNode.removeEventListener('scroll', setScrollTop);
			}
		};
	};
</script>

<div class:slc-table-main={true} class={containerClass} style:width style:height>
	{@render toolbar?.()}
	<div class:slc-table-container={true} class={tableContainerClass}>
		<div
			role="grid"
			bind:this={table.element}
			bind:clientHeight={table.clientHeight}
			use:scrollAction
			class:slc-table={true}
			class={tableClass}
			style:grid-template-rows={table.gridTemplateRows}
			style:grid-template-columns={table.gridTemplateColumns}
			{...attributes}
		>
			{@render thead?.()}

			{#each table.data as row, rowindex (row.id)}
				{@render tbody?.(row, rowindex)}
			{/each}

			{#each table.footers as foot, footerindex}
				{@render tfoot?.(foot, footerindex)}
			{/each}
		</div>
	</div>
	{@render statusbar?.()}
</div>

<style lang="postcss">
	.slc-table-main {
		@apply flex;
		@apply flex-col;
		@apply overflow-hidden;
	}
	.slc-table-container {
		@apply relative;
		@apply flex-1;
		@apply overflow-hidden;
	}
	.slc-table {
		@apply grid;
		@apply h-full;
		@apply w-full;
		@apply overflow-auto;
	}
</style>
