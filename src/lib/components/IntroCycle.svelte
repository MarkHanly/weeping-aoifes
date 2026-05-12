<script lang="ts">

  import data from '$lib/data/bbbc.json';

  type Episode = {
    epNum: number;
    date: string;
    name: string;
    intro: string;
    description: string;
  };

  function sampleArray<T>(arr: T[], n: number): T[] {
    const copy = [...arr];
    const result: T[] = [];

    for (let i = 0; i < n && copy.length > 0; i++) {
      const index = Math.floor(Math.random() * copy.length);
      result.push(copy.splice(index, 1)[0]);
    }

    return result;
  }

  const entries = $state(sampleArray(data as Episode[], 15));
  let index = $state(0);

    $effect(() => {
    if (entries.length === 0) return;

    const timer = setInterval(() => {
        index = (index + 1) % entries.length;
    }, 8000);

    return () => clearInterval(timer);
    });

</script>



<div class="text-white">{index}</div>

<div class="flex items-center justify-center h-full">
  {#key index}
    <p
      class="max-w-3xl text-4xl leading-relaxed text-center text-white
             animate-[fade-in-out_8s_ease-in-out_forwards]"
    >
      {entries[index]?.intro}
    </p>
  {/key}
</div>