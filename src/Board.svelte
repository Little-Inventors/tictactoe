<script>
  import Square from "./Square.svelte";
 
  let winner = null;
  let squares = [null, null, null, null, null, null, null, null, null];
  let xIsNext = true;
  $: status = "Next Player: " + (xIsNext ? "X" : "0");

  function restartGame() {
    squares = [null, null, null, null, null, null, null, null, null];
    xIsNext = true;
    winner = null;
  }

  function handleClick(i) {
    if (!squares[i]) {
      squares[i] = xIsNext ? "X" : "0";
      xIsNext = !xIsNext;
      winner = calculateWinner(squares);
    }
  }

  function calculateWinner(squares) {
    const winningCombo = [
      [0, 1, 2],
      [3, 4, 5],
      [6, 7, 8],
      [0, 3, 6],
      [1, 4, 7],
      [2, 5, 8],
      [0, 4, 8],
      [2, 4, 6]
    ];
    for (let i = 0; i < winningCombo.length; i++) {
      const [a, b, c] = winningCombo[i];
      if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c])
        return `Winner: ${squares[a]}`;
    }

    const isDraw = squares.every(square => square !== null);
    return isDraw ? "It's a draw" : null;
  }
</script>

<style>
  h3 {
    color: red;
  }
 
  .board {
    display: flex;
    flex-wrap: wrap;
    width: 300px;
  }
</style>

{#if winner}
  <h3>{winner}</h3>
{:else}
  <h3>{status}</h3>
{/if}

<div class="board">
  
    <Square value={squares[0]} handleClick={() => handleClick(0)} />
      <Square value={squares[1]} handleClick={() => handleClick(1)} />
        <Square value={squares[2]} handleClick={() => handleClick(2)} />
          <br>
          <Square value={squares[3]} handleClick={() => handleClick(3)} />
            <Square value={squares[4]} handleClick={() => handleClick(4)} />
              <Square value={squares[5]} handleClick={() => handleClick(5)} />
                <br>
                <Square value={squares[6]} handleClick={() => handleClick(6)} />
                  <Square value={squares[7]} handleClick={() => handleClick(7)} />
                    <Square value={squares[8]} handleClick={() => handleClick(8)} />
                      
  
</div>

{#if winner}
  <button on:click={restartGame}>Restart Game</button>
{/if}
