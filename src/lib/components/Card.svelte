<script>
    import rawEpisodes from '$lib/data/bbbc.json';
    import { Popover, Search, Button } from "flowbite-svelte";
    import { InfoCircleSolid, PlaySolid } from "flowbite-svelte-icons";
    
    const { className = "" } = $props()

    // Search term
    let searchTerm = $state("");

    let filteredEpisodes = $derived(
        ! searchTerm
            ? rawEpisodes 
            : rawEpisodes.filter(d =>
                    [
                    d.epNum?.toString(),
                    d.name,
                    d.date,
                    d.description
                    ].some(field =>
                    field?.toLowerCase().includes(searchTerm.toLowerCase())
                    )
                )

    )




</script>

<div class="${className}">

    <div class="w-[95%] md:w-[80%] lg:w-[66%] mx-auto py-6">
        <Search 
            clearable
            oninput={(e) => searchTerm = e.currentTarget.value}>
            <!-- <Button class="me-1 bg-rose-400 hover:bg-rose-500 cursor-pointer">Search</Button> -->
        </Search>
    
    </div>

    {#each filteredEpisodes as episode}
        <div class="flex w-[95%] md:w-[80%] lg:w-[66%] mx-auto my-2 p-4 gap-8 rounded-2xl bg-gradient-to-br from-sky-950 to-sky-800
        text-sm">

        <!-- Episode number + date -->
        <div class="flex items-center gap-4 text-left font-semibold text-slate-500">
            <span>#{episode.epNum}</span>
            <span>{episode.date}</span>
        </div>

        <!-- Episode name -->
        <div class="flex-1 text-gray-400 font-medium text-base leading-snug tracking-tight">
            {episode.name}
        </div>
        
        <!-- Caret icon -->
        <div class="flex items-start ml-auto">
            <InfoCircleSolid class="w-5 h-5 text-gray-500 cursor-pointer hover:text-gray-300 transition" />
            <Popover class="flex flex-col bg-slate-800  border-1 border-slate-200 max-w-md">
                <div class="text-slate-500 text-lg uppercase">{episode.name}</div>
                
                <div class="flex flex-row gap-2 text-xs text-slate-500 mb-2">
                    <span>#{episode.epNum}</span>
                    <span>{episode.date}</span>
                </div>
                
                <div class="flex-item text-slate-400 font-semibold mb-2">{episode.description}</div>
                <div class="flex-item text-slate-400 italic">{episode.intro}</div>
            </Popover>
        </div>

        <!-- Play button opens spotify link in new window -->
        <a target="_blank" href={episode['external_urls.spotify']}>
            <div class="bg-slate-100 rounded-full">
                <PlaySolid class="w-5 h-5 text-slate-800 cursor-pointer"/>
            </div>
        </a>

        </div>
    {/each}

</div>