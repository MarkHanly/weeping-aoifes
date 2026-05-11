<script lang="ts">
  import { Button, Modal, Skeleton } from "flowbite-svelte";
  import { SearchSolid, InfoCircleSolid, VolumeUpSolid, VolumeMuteSolid } from "flowbite-svelte-icons";
  import DataTableTest from "./DataTableTest.svelte";
  import audioFile from "$lib/assets/audio.m4a"
  
  // destructure AFTER typing
  let { sorting, onChangeSorting } = $props();
  
  let volumeOn = $state(false);
  let audioElement: HTMLAudioElement;
  let infoModal = $state(false);
  let searchModal = $state(false);


  function toggleAudio() {
    if (volumeOn) {
        volumeOn = false;
      audioElement?.pause();
    } else {
        volumeOn = true;
      audioElement?.play();
    }
  }

</script>

<!-- Hidden audio element -->
<audio bind:this={audioElement} src={audioFile} loop></audio>

<div class="bg-slate-950 sticky top-0 z-99">
  
    <div class="flex flex justify-between items-center p-2">

        <div class="flex text-slate-600 ml-4 uppercase text-lg font-semibold tracking-wide">
            weeping aoifes 
        </div>

        <div class="flex flex-row gap-2 items-center text-lg">

            <!-- The audiao button -->
            <Button onclick={toggleAudio}>
                {#if volumeOn}
                <VolumeUpSolid class="h-8 w-8 text-slate-600" />
                {/if}
                {#if !volumeOn}
                <VolumeMuteSolid class="h-8 w-8 text-slate-600" />
                {/if}
            </Button>

            <!-- The search button -->
             <Button onclick={() => (searchModal = true)}>
                <SearchSolid class="h-8 w-8 text-slate-600" />
            </Button>
            <Modal bind:open={searchModal} size="2xl" class="bg-slate-950/80 h-[90vh]">
                <DataTableTest className="flex-1" />
            </Modal>

            <!-- The info button -->
            <Button 
                onclick={() => (infoModal = true)}>
                <InfoCircleSolid class="h-8 w-8 text-slate-600" />
            </Button>
            <Modal title="About" bind:open={infoModal}>
                <Skeleton size="xl" class="my-8" />
            </Modal>


        </div>

    </div>

</div>

