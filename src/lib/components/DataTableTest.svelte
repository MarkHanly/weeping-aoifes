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
    perPage: 10,
    perPageSelect: [10, 25, 50, 100]
  };
</script>

<div class={"p-6 " + className}>
  <div class="mb-4">
    <h1 class="text-2xl font-semibold">Flowbite Svelte DataTable Test</h1>
    <p class="text-sm text-slate-500">Sortable and searchable demo of Flowbite Svelte Datatables.</p>
  </div>

  <div class="overflow-x-auto rounded-xl border border-slate-200 bg-white/80 p-4 shadow-sm dark:border-slate-800 dark:bg-slate-950/80">
    <Table dataTableOptions={options}>
      <TableHead {headItems} />
      <TableBody {bodyItems} />
    </Table>
  </div>
</div>
