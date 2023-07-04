<script>
    import Light from './light.svelte';

    let debug = false;
    
    let lights = [
        [true, true, true, true, true],
        [true, true, true, true, true],
        [true, true, true, true, true],
        [true, true, true, true, true],
        [true, true, true, true, true]];
    
    let hasWon = false;

    let state = "";

    let moves = 0;
    
    function handleClick(x, y) {
        if (hasWon) {
            return;
        }

        moves++;
        
        tryClick(x, y);
        tryClick(x-1, y);
        tryClick(x, y-1);
        tryClick(x+1, y);
        tryClick(x, y+1);

        checkGameState();
    }

    function tryClick(x, y) {
        if (x < 0 || y < 0 || x > 4 || y > 4) {
            return;
        }
        
        lights[x][y] = !lights[x][y];
    }

    function checkGameState() {
        state = ""
        let anyOn = false;
        for (let i = 0; i < 5; i++) {
          for (let j = 0; j < 5; j++) {
              anyOn ||= lights[i][j];
                state += "[" + i + ", " + j + "]: " + lights[i][j] + " ";
            }
        }

        hasWon = !anyOn;
    }

    function newGame() {
        do {
            for (let i = 0; i < 5; i++) {
              for (let j = 0; j < 5; j++) {
                  lights[i][j] = Math.random() < 0.5;
                }
            }
            checkGameState();
        } while (hasWon)

        moves = 0;
    }

    newGame();
</script>

<h2>More Lights off!</h2>
<p>Turn off all the lights to win.</p>
<div class="grid">
    <Light on={lights[0][0]} on:click={() => handleClick(0, 0)} />
    <Light on={lights[1][0]} on:click={() => handleClick(1, 0)} />
    <Light on={lights[2][0]} on:click={() => handleClick(2, 0)} />
    <Light on={lights[3][0]} on:click={() => handleClick(3, 0)} />
    <Light on={lights[4][0]} on:click={() => handleClick(4, 0)} />

    <Light on={lights[0][1]} on:click={() => handleClick(0, 1)} />
    <Light on={lights[1][1]} on:click={() => handleClick(1, 1)} />
    <Light on={lights[2][1]} on:click={() => handleClick(2, 1)} />
    <Light on={lights[3][1]} on:click={() => handleClick(3, 1)} />
    <Light on={lights[4][1]} on:click={() => handleClick(4, 1)} />

    <Light on={lights[0][2]} on:click={() => handleClick(0, 2)} />
    <Light on={lights[1][2]} on:click={() => handleClick(1, 2)} />
    <Light on={lights[2][2]} on:click={() => handleClick(2, 2)} />
    <Light on={lights[3][2]} on:click={() => handleClick(3, 2)} />
    <Light on={lights[4][2]} on:click={() => handleClick(4, 2)} />

    <Light on={lights[0][3]} on:click={() => handleClick(0, 3)} />
    <Light on={lights[1][3]} on:click={() => handleClick(1, 3)} />
    <Light on={lights[2][3]} on:click={() => handleClick(2, 3)} />
    <Light on={lights[3][3]} on:click={() => handleClick(3, 3)} />
    <Light on={lights[4][3]} on:click={() => handleClick(4, 3)} />

    <Light on={lights[0][4]} on:click={() => handleClick(0, 4)} />
    <Light on={lights[1][4]} on:click={() => handleClick(1, 4)} />
    <Light on={lights[2][4]} on:click={() => handleClick(2, 4)} />
    <Light on={lights[3][4]} on:click={() => handleClick(3, 4)} />
    <Light on={lights[4][4]} on:click={() => handleClick(4, 4)} />
</div>

{#if debug}
    <p>{state}</p>
{/if}
    
{#if hasWon}
    <p>You won in only {moves} moves! 🥳</p>
    <button on:click={newGame}>New Game</button>
{/if}

<style>
    .grid {
      display: grid;
      gap: 1px;
      grid-template-columns: repeat(5, 110px);
    }
</style>