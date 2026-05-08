<script lang="ts">
  import { Button, Modal, Skeleton } from "flowbite-svelte";
  import { SearchSolid, InfoCircleSolid, VolumeUpSolid, VolumeMuteSolid } from "flowbite-svelte-icons";
  import DataTableTest from "./DataTableTest.svelte";
  import audioFile from "$lib/assets/audio.m4a"
  
  // destructure AFTER typing
  let { sorting, onChangeSorting } = $props();
  
  let volumeOn = $state(false);
  let volume = $state(0);
  let audioElement: HTMLAudioElement;
  let infoModal = $state(false);
  let searchModal = $state(false);


  function handleVolumeChange(e: Event) {
    volume = parseFloat((e.target as HTMLInputElement).value);
    if (volume > 0) {
        volumeOn = true;
        audioElement?.play();
    }
    if (audioElement) {
      audioElement.volume = volume;
    }
  }

  function toggleAudio() {
    if (volumeOn) {
        volumeOn = false;
        volume = 0
      audioElement?.pause();
    } else {
        volumeOn = true;
        volume = 1
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

        <div class="flex flex-row gap-2 items-center">
            <Button class="text-lg" onclick={toggleAudio}>
                {#if volumeOn}
                <VolumeUpSolid class="h-8 w-8 text-slate-600" />
                {/if}
                {#if !volumeOn}
                <VolumeMuteSolid class="h-8 w-8 text-slate-600" />
                {/if}
            </Button>
            
            <input 
              type="range" 
              min="0" 
              max="1" 
              step="0.1" 
              bind:value={volume}
              onchange={handleVolumeChange}
              class="w-24 cursor-pointer accent-slate-600"
            />

             <Button class="text-lg" onclick={() => (searchModal = true)}>
                <SearchSolid class="h-8 w-8 text-slate-600" />
            </Button>
            <Modal bind:open={searchModal} size="2xl" class="bg-slate-950 h-[90vh]">
                <DataTableTest className="flex-1" />
            </Modal>

            <Button class="text-lg"
                onclick={() => (infoModal = true)}>
                <InfoCircleSolid class="h-8 w-8 text-slate-600" />
            </Button>
            <Modal title="About" bind:open={infoModal}>
                <Skeleton size="xl" class="my-8" />
            </Modal>


        </div>

    </div>

</div>

