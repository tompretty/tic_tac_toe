<script>
  import ScoreBoard from "./ScoreBoard.svelte";
  import GameBoard from "./GameBoard.svelte";
  import ResetButton from "./ResetButton.svelte";

  function newGameState() {
    return {
      board: ["", "", "", "", "", "", "", "", ""],
      gameOver: false,
      turn: "X",
      winningLine: []
    };
  }

  let state = newGameState();
  $: playables = state.board.map((_, i) => canPlay(i));

  let scores = {
    X: 0,
    O: 0
  };

  function makeMove(event) {
    let pos = event.detail.pos;

    if (canPlay(pos)) {
      play(pos);
      checkForWinner();
      checkForDraw();
      updateTurn();
    }
  }

  function canPlay(pos) {
    return state.board[pos] == "" && !state.gameOver;
  }

  function play(pos) {
    state.board[pos] = state.turn;
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
      let isWinningLine = line.every(i => state.board[i] == state.turn);
      if (isWinningLine) {
        state.gameOver = true;
        state.winningLine = line;
        scores[state.turn]++;
        break;
      }
    }
  }

  function checkForDraw() {
    if (state.board.every(s => s != "")) {
      console.log("draw");
      state.gameOver = true;
    }
  }

  function updateTurn() {
    state.turn = state.turn == "X" ? "O" : "X";
  }
</script>

<div class="container max-w-md mx-auto">
  <div class="mt-10">
    <ScoreBoard {...scores} />
  </div>
  <div class="mt-5">
    <GameBoard {...state} {playables} on:makeMove={makeMove} />
  </div>
  <div class="mt-5 flex justify-center">
    <ResetButton on:click={() => (state = newGameState())} />
  </div>
</div>
