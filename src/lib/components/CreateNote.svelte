<script lang="ts">
  import { Button } from "$lib/components/ui/button/index.js";
  import * as Drawer from "$lib/components/ui/drawer/index.js";
  import { Plus } from "svelte-radix";
  import Input from "./ui/input/input.svelte";
  import Textarea from "./ui/textarea/textarea.svelte";
</script>

<Drawer.Root>
  <Drawer.Trigger asChild let:builder>
    <Button builders={[builder]} variant="outline">
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
          <Input type="text" placeholder="Title" />
          <Textarea placeholder="Type your note here." rows={4} />
        </div>
      </div>
      <Drawer.Footer>
        <Button>Submit</Button>
        <Drawer.Close asChild let:builder>
          <Button builders={[builder]} variant="outline">Cancel</Button>
        </Drawer.Close>
      </Drawer.Footer>
    </div>
  </Drawer.Content>
</Drawer.Root>
