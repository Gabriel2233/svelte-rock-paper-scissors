<script>
  import { onMount, createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher();

  export let name;
  let image;

  onMount(() => {
    if (name === 'Rock') {
      image = '✊';
    } else if (name === 'Paper') {
      image = '✋';
    } else {
      image = '✌️';
    }
  });

  const onCardSelect = () => {
    dispatch('select-card', name);
  };
</script>

<div class="card-container" on:click={onCardSelect}>
  <h1 class="emoji">{image}</h1>
  <h3 class="name">{name}</h3>
</div>

<style>
  .card-container {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    padding: 4;
    border-radius: 8px;
    border: 2px solid #ddd;
    background: #fff;
    transform: background 0.3s ease;
    cursor: pointer;
  }

  .card-container:hover {
    background: rgba(226, 226, 226, 0.5);
  }

  .name {
    font-weight: 600;
    font-size: 1em;
    padding-bottom: 1em;
  }

  .emoji {
    font-size: 3em;
    padding-top: 0.5em;
    padding-bottom: 0.5em;
  }
</style>
