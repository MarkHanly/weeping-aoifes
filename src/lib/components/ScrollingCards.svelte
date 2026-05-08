<script>

  import { Card } from "flowbite-svelte";
  const { episodes } = $props();

</script>

<div class="grid gap-4">
  {#each episodes as ep}

  <div class="h-screen">

    <Card 
    class="relative flex place-items-center text-center justify-center p-6 
    w-[100%] h-[80vh] m-auto rounded bg-slate-600 text-4xl sticky 
    top-1 z-10 hover:hover:bg-slate-700">
        <p class="absolute top-4 right-4 text-xl text-slate-800">#{ep.epNum}</p>    
        <p class="font-['Doto',cursive] text-pink-200">{ep.intro}</p>
    
    </Card>

    </div>
  
  {/each}
</div>