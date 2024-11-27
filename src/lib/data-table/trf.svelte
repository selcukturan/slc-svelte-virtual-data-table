<script lang="ts" generics="TData extends Row">
	import type { Row } from './types';
	import type { HTMLAttributes } from 'svelte/elements';
	import type { Snippet } from 'svelte';
	import { getTable } from './tables.svelte';

	type Props = HTMLAttributes<HTMLDivElement> & {
		data?: TData[];
		children: Snippet;
		fi?: number;
		class?: string;
	};
	const { data, children, fi, class: classes, ...attributes }: Props = $props();

	const table = getTable<TData>();
</script>

<div
	role="row"
	class:slc-table-trf={true}
	class={classes}
	style:--slc-grid-row-start={table.setData && table.setData.length > 0
		? table.setData.length + table.headerRowCount + table.footerRowCount
		: 2}
	data-originalrowindex={fi}
	{...attributes}
>
	{@render children?.()}
</div>

<style lang="postcss">
	.slc-table-trf {
		@apply contents;
	}
</style>
