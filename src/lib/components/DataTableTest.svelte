<script lang="ts">
  import { Table, TableHead, TableBody } from "@flowbite-svelte-plugins/datatable";
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

  const headItems = ["Number", "Release Date", "Name", "Intro"];
  const bodyItems = items.map((item) => [item.epNum, item.release_date, item.name, item.intro]);

  const options: DataTableOptions = {
    searchable: true,
    sortable: true,
    paging: true,
    perPage: 50,
    perPageSelect: [10, 25, 50, 100]
  };



</script>

<div class={"p-6" + className}>
  <div class="overflow-x-auto rounded-xl border border-slate-900 text-slate-50 p-16 shadow-sm">
    <Table dataTableOptions={options}>
      <TableHead {headItems} />
      <TableBody {bodyItems} />
    </Table>
  </div>
</div>

<style>
  :global(nav.datatable-pagination) {
    display: flex !important;
    flex-direction: row !important;
    justify-content: center !important;
    align-items: center !important;
    flex-wrap: nowrap !important;
  }

  :global(.datatable-table tbody td) {
    vertical-align: top !important;
  }
</style>