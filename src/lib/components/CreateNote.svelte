<script lang="ts">
  import { Button } from "$lib/components/ui/button/index.js";
  import * as Drawer from "$lib/components/ui/drawer/index.js";
  import { Plus } from "svelte-radix";
  import Input from "./ui/input/input.svelte";
  import Textarea from "./ui/textarea/textarea.svelte";
  import axios from "axios";
  import { createEventDispatcher } from "svelte";

  type NoteTypes = {
    message: string;
    note: {
      title: string;
      description: string;
      _id: string;
      __v: number;
    };
  };

  const dispatch = createEventDispatcher();

  let data: NoteTypes;

  let title = "";
  let description = "";
  let error;
  let success: boolean;
  let drawerIsOpen: boolean;

  const handleCreateNote = async () => {
    dispatch("isLoading", true);
    drawerIsOpen = false;

    try {
      const response = await axios.post<NoteTypes>(
        "http://localhost:3000/note",
        {
          title: title,
          description: description,
        }
      );

      data = response.data;
      dispatch("dataReceived", data);
      dispatch("isLoading", false);
      title = "";
      description = "";
    } catch (e) {
      error = e;
    }
  };
</script>

<Drawer.Root open={drawerIsOpen}>
  <Drawer.Trigger asChild let:builder>
    <Button
      builders={[builder]}
      variant="outline"
      on:click={() => (drawerIsOpen = true)}
    >
      <Plus class="mr-2 h-4 w-4" />
      Add Note
    </Button>
  </Drawer.Trigger>
  <Drawer.Content>
    <div class="mx-auto w-full max-w-sm">
      <Drawer.Header>
        <Drawer.Title>Create Your Note</Drawer.Title>
        <Drawer.Description>Set your daily activity.</Drawer.Description>
      </Drawer.Header>
      <div class="p-4 pb-0">
        <div class="flex flex-col items-center justify-center gap-3">
          <Input bind:value={title} type="text" placeholder="Title" />
          <Textarea
            bind:value={description}
            placeholder="Type your note here."
            rows={4}
          />
        </div>
      </div>
      <Drawer.Footer>
        <Button on:click={handleCreateNote}>Submit</Button>
        <Drawer.Close asChild let:builder>
          <Button builders={[builder]} variant="outline">Cancel</Button>
        </Drawer.Close>
      </Drawer.Footer>
    </div>
  </Drawer.Content>
</Drawer.Root>
