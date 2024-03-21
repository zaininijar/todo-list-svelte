<script lang="ts">
  import Rocket from "svelte-radix/Rocket.svelte";
  import * as Alert from "$lib/components/ui/alert/index.js";
  import Navigation from "$lib/components/Navigation.svelte";
  import Table from "$lib/components/Table.svelte";
  import CreateNote from "$lib/components/CreateNote.svelte";
  import ListNote from "$lib/components/ListNote.svelte";

  let isShowAlert = false;

  let notes = [
    {
      title: "Note 1 title",
      description: "Note 1 description",
    },
    {
      title: "Note 2 title",
      description:
        "Yes. Free to use for personal and commercial projects. No attribution required.",
    },
  ];
</script>

<main>
  <div class="px-4">
    <Navigation />
    <CreateNote />
    {#if isShowAlert}
      <Alert.Root class="mt-2">
        <Rocket class="h-4 w-4" />
        <Alert.Title>Heads up!</Alert.Title>
        <Alert.Description
          >You can add components to your app using the cli.</Alert.Description
        >
      </Alert.Root>
    {/if}
    <div class="flex flex-col gap-2 mt-4">
      {#each notes as note}
        <ListNote {...note} />
      {/each}
    </div>
  </div>
</main>

<style>
</style>
