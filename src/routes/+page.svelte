<script lang="ts">
  import { enhance } from "$app/forms";
  import { fade } from "svelte/transition";
  import Item from "./Item.svelte";

  let items = $state<any[]>([]);
  let search = $state(1);

  function executeSearch({ cancel, formData: data }: any) {
    cancel();

    search++;
    items = Array.from({ length: 30 }).map((_, idx) => ({
      id: idx + 1,
      name: "Item " + idx + 1,
    }));
  }

  function remove(toRemove: any) {
    items = items.filter((item) => item.id != toRemove.id);
  }
</script>

<div class="p-6">
  <form method="post" use:enhance={executeSearch}>
    <div class="flex flex-col gap-3">
      <div>
        <button class="border p-3">Search</button>
      </div>
      <div>
        {#if items.length}
          {#key search}
            <div in:fade|local out:fade|local class="flex flex-col min-w-0">
              {#each items as item (item.id)}
                <Item {item} {remove} />
              {/each}
            </div>
          {/key}
        {/if}
      </div>
    </div>
  </form>
</div>
