<script>
  import Card from './Card.svelte';
  import GameData from './GameData.svelte';

  let hasStarted = false;
  let points = [0, 0];
  let currentTurn = 0;
  let currentMatch = [];
  const options = ['Rock', 'Paper', 'Scissors'];

  /*
		Logic:

		User can start the game

		Rules:

		Rock beats Scissors
		Paper beats Rock
		Scissors beat Paper

		Draw - points for both
	*/

  const startGame = () => {
    hasStarted = !hasStarted;
  };

  const onUserSelect = (e) => {
    currentMatch = [...currentMatch, e.detail];

    currentTurn = 1;

    const result = onBotSelect();
    currentMatch = [...currentMatch, result];

    console.log(currentMatch);

    checkResult(currentMatch);
    currentMatch = [];
    currentTurn = 0;
  };

  const onBotSelect = () => {
    const randomNum = Math.floor(Math.random() * 3);

    return options[randomNum];
  };

  const checkResult = (match) => {
    console.log(match[0], match[1]);
    if (match[0] === 'Paper' && match[1] === 'Rock') {
      points[0] += 1;
    } else if (match[0] === 'Paper' && match[1] === 'Scissors') {
      points[1] += 1;
    } else if (match[0] === 'Rock' && match[1] === 'Paper') {
      points[1] += 1;
    } else if (match[0] === 'Rock' && match[1] === 'Scissors') {
      points[0] += 1;
    } else if (match[0] === 'Scissors' && match[1] === 'Rock') {
      points[1] += 1;
    } else if (match[0] === 'Scissors' && match[1] === 'Paper') {
      points[0] += 1;
    } else {
      points[0] = points[0];
      points[1] = points[1];
    }
  };
</script>

<div class="main">
  <h1 class="heading">Svelte Rock Paper Scissors</h1>

  <div class="options-container">
    {#each options as option}
      <Card name={option} on:select-card={onUserSelect} />
    {/each}
  </div>

  <div class="game-container">
    {#if hasStarted}
      {#each points as point, index}
        <GameData turn={currentTurn} {point} player={index} />
      {/each}
    {:else}
      <button on:click={startGame} class="start-btn">Start Game</button>
    {/if}
  </div>

  <p>{points[0]} {points[1]}</p>
</div>

<style>
  .main {
    width: 100vw;
    height: 100vh;

    display: flex;
    align-items: center;
    flex-direction: column;
  }

  .heading {
    font-weight: 900;
    font-size: 1.5em;
    color: #333;
    padding: 2em 0;
  }

  .options-container {
    width: 90%;
    max-width: 980px;
    margin: 0 auto;

    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 20px;
  }

  .start-btn {
    display: flex;
    align-self: center;
    justify-self: center;
    padding: 8px;
    border-radius: 4px;
    color: #fff;
    background: #0070f3;
    border: none;
    font-size: 1em;
    font-weight: 600;
  }

  .game-container {
    width: 1026px;
    padding-top: 3em;
    display: flex;
    align-items: center;
    justify-content: center;
  }
</style>
