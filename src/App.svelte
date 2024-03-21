<script lang="ts">
  import Rocket from "svelte-radix/Rocket.svelte";
  import * as Alert from "$lib/components/ui/alert/index.js";
  import Navigation from "$lib/components/Navigation.svelte";
  import CreateNote from "$lib/components/CreateNote.svelte";
  import ListNote from "$lib/components/ListNote.svelte";

  import { onMount } from "svelte";
  import axios from "axios";
  import { Skeleton } from "$lib/components/ui/skeleton";

  let notes: Array<{
    title: string;
    description: string;
  }> = [];

  let error;

  let isLoading = false;
  let isSuccess = false;
  let successMessage: string;

  onMount(async () => {
    isLoading = true;

    try {
      const res = await axios.get("http://localhost:3000/note");
      notes = res.data;
    } catch (e) {
      error = e;
    }

    isLoading = false;
  });

  const getNote = async () => {
    isLoading = true;

    try {
      const res = await axios.get("http://localhost:3000/note");
      notes = res.data;
    } catch (e) {
      error = e;
    }

    isLoading = false;
  };

  const handleDataReceived = (event: any) => {
    isSuccess = event.detail !== null;
    successMessage = event.detail.message;
    getNote();
  };

  const handleLoading = (event: any) => {
    isLoading = event.detail;
  };
</script>

<main>
  <div class="px-4">
    <Navigation />

    <CreateNote
      on:dataReceived={handleDataReceived}
      on:isLoading={handleLoading}
    />
    {#if isSuccess}
      <Alert.Root class="mt-2">
        <Rocket class="h-4 w-4" />
        <Alert.Title>Great !</Alert.Title>
        <Alert.Description>
          {successMessage}
        </Alert.Description>
      </Alert.Root>
    {/if}
    <div class="flex flex-col gap-2 mt-4">
      {#if !isLoading}
        {#each notes as note}
          <ListNote {...note} />
        {/each}
      {:else}
        {#each [1, 2, 3, 4] as times}
          <Skeleton class="h-[40px] w-full rounded-md" />
        {/each}
      {/if}
    </div>
  </div>
</main>

<style>
</style>
