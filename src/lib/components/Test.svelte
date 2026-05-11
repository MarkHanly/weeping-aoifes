<script lang="ts"> // lang="ts" ensures we are using typescript

  const { class: className = '' } = $props(); // reads in class as a prop named className

  import data from '$lib/data/bbbc.json'; // Loads the data

  type Episode = { // Defines the types for the episode data
    epNum: number;
    release_date: string;
    name: string;
    intro: string;
  };


  let index = $state(0); // Initialises the index at 0

  // This is a reactive block that runs when entries on index changes

  $effect(() => {

    const timer = setInterval(() => {
        index = (index + 1) % entries.length;
    }, 10000);

    return () => clearInterval(timer); 
  });


  // Function to sample {n} items from array {arr}
  function sampleArray<T>(arr: T[], n: number): T[] { 
    const copy = [...arr];
    const result: T[] = [];

    for (let i = 0; i < n && copy.length > 0; i++) {
      const index = Math.floor(Math.random() * copy.length);
      result.push(copy.splice(index, 1)[0]);
    }

    return result;
  }

  const entries = $state(sampleArray(data as Episode[], 30)); // Samples 30 episodes


</script>

<main class={`flex flex-col h-full ${className}`}>
  <!-- Internal header -->
  <!-- <div class="h-10 test-banner"></div> -->

  <!-- This is where the keyframes is applied. Note bg-sunset is defined in app.css -->
    <div class="flex-1 daycycle-bg flex items-center justify-center"> 

      {#key index}
        <p
          class="max-w-4xl px-4 text-[clamp(1.5rem,3.5vw,3.5rem)] leading-relaxed 
                text-center font-['Doto',cursive] break-words animate-[fade-in-out_10s_forwards]">
          {entries[index]?.intro}
        </p>
      {/key}

  </div>

</main>

<style>
  :global {
    @keyframes fade-in-out {
      0%   { opacity: 0; }
      25%  { opacity: 1; }
      75%  { opacity: 1; }
      100% { opacity: 0; }
    }
  }
</style>
