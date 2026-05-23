<script lang="ts">
  import { Button, Modal, Skeleton } from "flowbite-svelte";
  import { SearchSolid, InfoCircleSolid, VolumeUpSolid, VolumeMuteSolid, HomeSolid } from "flowbite-svelte-icons";
  import audioFile from "$lib/assets/audio.m4a"

  let volumeOn = $state(false);
  let audioElement: HTMLAudioElement;
  let infoModal = $state(false);

    async function toggleAudio() {
    if (!audioElement) return;

    try {
        if (volumeOn) {
        volumeOn = false;
        audioElement.pause();
        } else {
        volumeOn = true;
        await audioElement.play(); // ✅ important
        }
    } catch (err) {
        console.error("Audio play failed:", err);
    }
    }

</script>

<!-- Hidden audio element -->
<audio bind:this={audioElement} src={audioFile} loop></audio>

<div class="bg-slate-950 sticky top-0 z-99">
  
    <div class="flex flex justify-between items-center p-2">

        <a href="/" class="flex items-center gap-1">
            <HomeSolid class="h-8 w-8 text-slate-600" />
            <span class="flex text-slate-600 uppercase text-lg font-semibold tracking-wide inline">
                weeping aoifes
            </span>
            </a>
        

        <div class="flex flex-row gap-2 items-center text-lg">

            <!-- The audio button -->
            <Button onclick={toggleAudio}>
                {#if volumeOn}
                    <VolumeUpSolid class="h-8 w-8 text-slate-600" />
                {/if}

                {#if !volumeOn}
                    <VolumeMuteSolid class="h-8 w-8 text-slate-600" />
                {/if}
            </Button>

            <!-- The search button -->
            <a href="/search">
                <SearchSolid class="h-8 w-8 text-slate-600" />
            </a>

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

