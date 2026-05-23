<script lang="ts">
  import Main from '$lib/components/Main.svelte';
  import rawEpisodes from '$lib/data/bbbc.json';

  function shuffle<T>(array: T[]) {
    return [...array].sort(() => Math.random() - 0.5);
  }

  let randomEpisodes = $state(shuffle(rawEpisodes));

  // sorting state (1 = random, 2 = oldest, 3 = newest)
  let sorting = $state(3);

  function setSorting(value: number) {
		sorting = value;
	};

  // derived, reactive episodes
    // const episodes = $derived(() => {
    // switch (sorting) {
    //     case 1:
    //     return randomEpisodes;
    //     case 2:
    //     return [...rawEpisodes].sort((a, b) => a.epNum - b.epNum);
    //     case 3:
    //     return [...rawEpisodes].sort((a, b) => b.epNum - a.epNum);
    // }
    // });

</script>


<!-- Pass sorting *down* AND allow a callback -->
 <div class="min-h-screen flex flex-col">
    <Main class="flex-1"/>
</div>

