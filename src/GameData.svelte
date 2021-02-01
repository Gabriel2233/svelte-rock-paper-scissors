<script>
  export let turn;
  export let point;
  export let player;
</script>

<div class="main">
  <h3>
    {#if turn === player}
      {#if player === 1}
        Bot's Turn
      {:else}
        Your Turn
      {/if}
    {:else}
      Bot's
    {/if}
  </h3>

  <h1>{point} points</h1>
</div>

<style>
  .main {
    border: 2px solid #ddd;
    border-radius: 8px;
    margin: 0 2em;
    width: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .main h1 {
    font-weight: 800;
    margin: 1em 0;
    padding: 6px;
  }

  .main h3 {
    font-weight: 500;
    font-size: 1em;
    margin: 1em 0;
    padding: 6px;
  }
</style>
