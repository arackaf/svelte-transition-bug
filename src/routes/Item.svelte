<script lang="ts">
  import { fade } from "svelte/transition";

  let { item, remove }: any = $props();
</script>

<div out:fade|local class="flex gap-3 p-3">
  <span>{item.name}</span>
  <button onclick={() => remove(item)}>Remove</button>
</div>
