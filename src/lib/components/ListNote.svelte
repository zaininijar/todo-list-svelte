<script lang="ts">
  import * as Collapsible from "$lib/components/ui/collapsible";
  import { Pencil1, Trash } from "svelte-radix";
  import Button from "./ui/button/button.svelte";

  export let title: string;
  export let description: string;
</script>

<Collapsible.Root>
  <div class="border rounded-md p-2">
    <Collapsible.Trigger class="min-w-full flex justify-between items-center">
      <div class="font-bold text-sm">{title}</div>
      <div>
        <Button variant="outline" size="icon">
          <Pencil1 class="h-4 w-4" />
        </Button>
        <Button variant="outline" size="icon" class="text-red-400">
          <Trash class="h-4 w-4" />
        </Button>
      </div>
    </Collapsible.Trigger>
    <Collapsible.Content>
      <div class="text-sm">
        {description}
      </div>
    </Collapsible.Content>
  </div>
</Collapsible.Root>
