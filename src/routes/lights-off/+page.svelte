<script>
    import Light from './light.svelte';

    let debug = false;
    
    let lights = [
        [true, true, true],
        [true, true, true],
        [true, true, true]];
    
    let hasWon = false;

    let state = "";
    
    function handleClick(x, y) {
        if (hasWon) {
            return;
        }
        
        tryClick(x, y);
        tryClick(x-1, y);
        tryClick(x, y-1);
        tryClick(x+1, y);
        tryClick(x, y+1);

        checkGameState();
    }

    function tryClick(x, y) {
        if (x < 0 || y < 0 || x > 2 || y > 2) {
            return;
        }
        
        lights[x][y] = !lights[x][y];
    }

    function checkGameState() {
        state = ""
        let anyOn = false;
        for (let i = 0; i < 3; i++) {
          for (let j = 0; j < 3; j++) {
              anyOn ||= lights[i][j];
                state += "[" + i + ", " + j + "]: " + lights[i][j] + " ";
            }
        }

        hasWon = !anyOn;
    }

    function newGame() {
        do {
            for (let i = 0; i < 3; i++) {
              for (let j = 0; j < 3; j++) {
                  lights[i][j] = Math.random() < 0.5;
                }
            }
            checkGameState();
        } while (hasWon)
    }

    newGame();
</script>

<h1>Lights off!</h1>
<p>Turn off all the lights to win.</p>
<div class="grid">
    <Light on={lights[0][0]} on:click={() => handleClick(0, 0)} />
    <Light on={lights[1][0]} on:click={() => handleClick(1, 0)} />
    <Light on={lights[2][0]} on:click={() => handleClick(2, 0)} />
    <Light on={lights[0][1]} on:click={() => handleClick(0, 1)} />
    <Light on={lights[1][1]} on:click={() => handleClick(1, 1)} />
    <Light on={lights[2][1]} on:click={() => handleClick(2, 1)} />
    <Light on={lights[0][2]} on:click={() => handleClick(0, 2)} />
    <Light on={lights[1][2]} on:click={() => handleClick(1, 2)} />
    <Light on={lights[2][2]} on:click={() => handleClick(2, 2)} />
</div>

{#if debug}
    <p>{state}</p>
{/if}
    
{#if hasWon}
    <p>You win! 🥳</p>
    <button on:click={newGame}>New Game</button>
{/if}

<style>
    .grid {
      display: grid;
      gap: 1px;
      grid-template-columns: repeat(3, 110px);
    }
</style>