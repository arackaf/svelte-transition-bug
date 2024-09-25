<script lang="ts">
  import { enhance } from "$app/forms";

  let items = $state<any[]>([]);

  function executeSearch({ cancel, formData: data }: any) {
    cancel();

    items = Array.from({ length: 30 }).map((_, idx) => ({
      id: idx + 1,
      name: "Item " + idx + 1,
    }));
  }
</script>

<form method="post" use:enhance={executeSearch}>
  <button>Search</button>
  {#each items as item}
    <div>{item.name}</div>
  {/each}
</form>
