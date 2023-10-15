<script lang="ts">
    import iconTrash from "@iconify-icons/ic/outline-delete";
    import { Dialog } from "m3-svelte";
    import { Button } from "m3-svelte";
  
    let open = false;
  </script>
  
    <h2 class="m3-font-headline-large">Dialog</h2>
    <div class="area">
      <Button type="tonal" on:click={() => (open = true)}>Open</Button>
      <Dialog icon={iconTrash} headline="Permanently delete?" bind:open>
        Deleting the selected messages will also remove them from all synced devices.
        <svelte:fragment slot="buttons">
          <Button type="text" on:click={() => (open = false)}>Cancel</Button>
          <Button type="tonal" on:click={() => (open = false)}>Delete</Button>
        </svelte:fragment>
      </Dialog>
    </div>
  
  <style>
    :global(body) {
      margin: 0;
    }

    .area {
      margin: auto -1rem -1rem -1rem;
      padding: 1rem;
    }
    h2 {
      margin-top: 0;
      margin-bottom: 1rem;
    }
  </style>