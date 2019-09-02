<script>
  import ScoreBoard from "./ScoreBoard.svelte";
  import GameBoard from "./GameBoard.svelte";
  import ResetButton from "./ResetButton.svelte";

  let board = ["", "", "", "", "", "", "", "", ""];
  let gameOver = false;
  let turn = "X";
  let winningLine = [];
  let scores = {
    noughts: 0,
    crosses: 0
  };

  function newGame() {
    board = ["", "", "", "", "", "", "", "", ""];
    gameOver = false;
    turn = "X";
    winningLine = [];
  }

  function makeMove(event) {
    let pos = event.detail.pos;

    if (canPlay(pos)) {
      play(pos);
      checkForWinner();
      checkForDraw();
      updateTurn();
    }
  }

  $: canPlay = pos => board[pos] == "" && !gameOver;

  function play(pos) {
    board[pos] = turn;
  }

  function checkForWinner() {
    let lines = [
      [0, 1, 2],
      [3, 4, 5],
      [6, 7, 8],
      [0, 3, 6],
      [1, 4, 7],
      [2, 5, 8],
      [0, 4, 8],
      [6, 4, 2]
    ];

    for (var line of lines) {
      let isWinningLine = line.every(i => board[i] == turn);
      if (isWinningLine) {
        gameOver = true;
        winningLine = line;
        if (turn == "X") {
          scores.crosses++;
        } else {
          scores.noughts++;
        }
        break;
      }
    }
  }

  function checkForDraw() {
    if (board.every(s => s != "")) {
      console.log("draw");
      gameOver = true;
    }
  }

  function updateTurn() {
    turn = turn == "X" ? "O" : "X";
  }
</script>

<div class="container max-w-md mx-auto">
  <div class="mt-10">
    <ScoreBoard {scores} />
  </div>
  <div class="mt-5">
    <GameBoard
      {board}
      {canPlay}
      {gameOver}
      {winningLine}
      on:makeMove={makeMove} />
  </div>
  <div class="mt-5 flex justify-center">
    <ResetButton on:click={newGame} />
  </div>
</div>
