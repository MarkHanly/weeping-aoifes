<script lang="ts">
  import Header from '$lib/components/Header.svelte';
  import Test from '$lib/components/Test.svelte';
  import ScrollingCards from '$lib/components/ScrollingCards.svelte';
  import FlipCard from '$lib/components/FlipCard.svelte';
  import DataTableTest from '$lib/components/DataTableTest.svelte';
  import IntroCycle from '$lib/components/IntroCycle.svelte';
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
    const episodes = $derived(() => {
    switch (sorting) {
        case 1:
        return randomEpisodes;
        case 2:
        return [...rawEpisodes].sort((a, b) => a.epNum - b.epNum);
        case 3:
        return [...rawEpisodes].sort((a, b) => b.epNum - a.epNum);
    }
    });

</script>


<!-- Pass sorting *down* AND allow a callback -->
 <div class="min-h-screen flex flex-col">
    <Header {sorting} onChangeSorting={setSorting} />
    <Test class="flex-1"/>
</div>

