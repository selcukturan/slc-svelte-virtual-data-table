<script lang="ts" generics="TData extends Row">
	import { setTable, type Settings, type Row } from '../tables.svelte';
	import { Table, Th, Td, Tf, Trh, Trd, Trf } from '../';

	const { data, settings }: { data: TData[]; settings: Settings<TData> } = $props();
	const table = setTable<TData>(data, settings);

	$effect(() => {
		if (data) table.setData = data;
		if (settings) table.setSettings = settings;
	});
</script>

<!-- prettier-ignore -->
<Table {data} class="bg-slate-50 dark:bg-slate-950" width={`100%`} height={`100%`}>
	{#snippet thead()}
		<Trh>
			{#each table.columns as col, ci (col.field)}
				<Th {data} {col} {ci} class="border-slate-300 bg-slate-100 dark:border-slate-600 dark:bg-slate-800">
					{col.label}
				</Th>
			{/each}
		</Trh>
	{/snippet}
	{#snippet tbody(row, ri)}
		<Trd {row} {ri}>
			{#each table.columns as col, ci (col.field)}
				<Td {col} {ci} {row} {ri} class="border-slate-200 dark:border-slate-700">
					{row[col.field]}
				</Td>
			{/each}
		</Trd>
	{/snippet}
	{#snippet tfoot(foot, fi)}
		<Trf {data} {fi}>
			{#each table.columns as col, ci (col.field)}
				<Tf {data} {col} {ci} {foot} {fi} class="border-slate-300 bg-slate-100 dark:border-slate-600 dark:bg-slate-800">
					{foot[table.columns[ci].field]}
				</Tf>
			{/each}
		</Trf>
	{/snippet}
</Table>
