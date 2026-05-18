<script>
    import rawEpisodes from '$lib/data/bbbc.json';
    import { CaretDownSolid } from "flowbite-svelte-icons";
    
    const { className = "" } = $props();

</script>

<div class="${className}">

    {#each rawEpisodes as episode}
    <div class="flex w-[95%] md:w-[80%] lg:w-[66%] mx-auto my-2 p-4 gap-8 rounded-2xl bg-gradient-to-br from-slate-950 to-slate-800
    text-sm">

    <!-- Episode number + date -->
    <div class="flex flex-col text-left text-xs font-semibold text-gray-400 shrink-0">
        <span>#{episode.epNum}</span>
        <span>{episode.date}</span>
    </div>

    <!-- Episode name -->
    <div class="flex-1 text-gray-400 font-medium text-base leading-snug tracking-tight">
        {episode.name}
    </div>

    <!-- Caret icon -->
    <div class="flex items-start ml-auto">
        <CaretDownSolid class="w-5 h-5 text-gray-500 cursor-pointer hover:text-gray-300 transition" />
    </div>

    </div>
    {/each}

</div>