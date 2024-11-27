<script lang="ts" generics="TData extends Row">
	import type { Row } from './types';
	import type { HTMLAttributes } from 'svelte/elements';
	import type { Snippet } from 'svelte';
	import { getTable } from './tables.svelte';

	type Props = HTMLAttributes<HTMLDivElement> & {
		children: Snippet;
		class?: string;
		ri?: number;
		row?: TData;
	};
	const { children, class: classes, ri, row, ...attributes }: Props = $props();

	const table = getTable<TData>();

	const originalRowIndex =
		row?.originalRowIndex !== null && row?.originalRowIndex !== undefined
			? +row.originalRowIndex
			: undefined;
	const gridRowStart =
		originalRowIndex !== undefined
			? originalRowIndex + table.headerRowCount + table.footerRowCount
			: undefined;
</script>

<div
	role="row"
	class:slc-table-trd={true}
	class={classes}
	style:--slc-grid-row-start={gridRowStart}
	aria-rowindex={ri}
	data-originalrowindex={originalRowIndex}
	{...attributes}
>
	{@render children?.()}
</div>

<style lang="postcss">
	.slc-table-trd {
		@apply contents;
	}
</style>
