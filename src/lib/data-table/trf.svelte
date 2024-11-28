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

	const gridRowStart = $derived(
		table.setData.length + table.headerRowCount + (fi === undefined ? 0 : fi) + 1
	);
</script>

<div
	role="row"
	class:slc-table-trf={true}
	class={classes}
	style:--slc-grid-row-start={gridRowStart}
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
