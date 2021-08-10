<script>
  import Card from "./Card.svelte";

  export let items;
</script>

<div>
  {#each items as item}
    <div class="row">
      <div class="col">
        <Card {item} />
      </div>
    </div>
  {/each}
</div>
