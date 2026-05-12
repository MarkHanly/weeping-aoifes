<script lang="ts">
  import { Table, TableBody, TableBodyCell, TableBodyRow, TableHead, TableHeadCell } from "@flowbite-svelte-plugins/datatable";
  import type { DataTableOptions } from "@flowbite-svelte-plugins/datatable";
  import episodes from "$lib/data/bbbc.json";

  const { className = "" } = $props();

  type Episode = {
    epNum: number;
    date: string;
    name: string;
    intro: string;
    description: string;
  };

  const items: Episode[] = episodes as Episode[];

  const bodyItems = items.map((item) => [item.epNum, item.date, item.name, item.intro, item.description]);

  const options: DataTableOptions = {
    searchable: true,
    sortable: true,
    paging: false,
    striped: true,
    scrollY: "70vh",
    fixedColumns: true,
    locale: 'en-IE'
  };



</script>

<div class={className}>
  <div class="overflow-x-auto">

<Table
  dataTableOptions={options}
  class="w-full table-fixed">
  <TableHead>
    <TableHeadCell class="w-18 text-left">Number</TableHeadCell>
    <TableHeadCell class="w-48 text-left">Date</TableHeadCell>
    <TableHeadCell class="w-64 text-left">Title</TableHeadCell>
    <TableHeadCell class="w-156 text-left">Intro</TableHeadCell>
    <TableHeadCell class="text-left">Description</TableHeadCell>
  </TableHead>
  <TableBody 
    class="m-64"
   {bodyItems}> 
  </TableBody>
</Table>

  </div>
</div>
