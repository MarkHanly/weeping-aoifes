<script lang="ts">
  import { Table, TableHead, TableBody} from "@flowbite-svelte-plugins/datatable";
  import { P, Heading } from "flowbite-svelte";
  import type { DataTableOptions } from "@flowbite-svelte-plugins/datatable";
  import episodes from "$lib/data/bbbc.json";

  const { className = "" } = $props();

  type Episode = {
    epNum: number;
    release_date: string;
    name: string;
    intro: string;
  };

  const items: Episode[] = episodes as Episode[];

  const headItems = [
    { text: 'Number', class: 'w-64' },
    { text: 'Release Date', class: 'w-32' },
    { text: 'Name', class: 'w-64' },
    { text: 'Intro', class: 'w-auto' }
  ];

  const bodyItems = items.map((item) => [item.epNum, item.release_date, item.name, item.intro]);

  const options: DataTableOptions = {
    searchable: true,
    sortable: true,
    paging: true,
    perPage: 50,
    perPageSelect: [10, 25, 50, 100]
  };



</script>

<div class={className}>
  <div class="overflow-x-auto">

<Table
  dataTableOptions={options}
  class="w-full table-fixed">
  <TableHead {headItems} />
  <TableBody {bodyItems} />
</Table>

    <!-- <Table dataTableOptions={options}>
      <TableHead {headItems} />
      <TableBody {bodyItems} /> 
    </Table> -->
  </div>
</div>
