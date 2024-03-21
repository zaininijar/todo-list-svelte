<script lang="ts">
  import * as Collapsible from "$lib/components/ui/collapsible";

  export let title: string;
  export let description: string;
</script>

<Collapsible.Root>
  <div class="border rounded-md p-2">
    <Collapsible.Trigger>
      <div class="font-bold text-sm">{title}</div>
    </Collapsible.Trigger>
    <Collapsible.Content>
      <div class="text-sm">
        {description}
      </div>
    </Collapsible.Content>
  </div>
</Collapsible.Root>
