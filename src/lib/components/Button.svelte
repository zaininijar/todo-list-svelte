<script lang="ts">
  import { Button } from "$lib/components/ui/button/index.js";
  import { Plus } from "svelte-radix";

  export let additional: any;

  export let props: { title: string } = {
    title: "Button",
  };
</script>

<Button {...additional}>
  <Plus class="mr-2 h-4 w-4" />
  {props.title}
</Button>
