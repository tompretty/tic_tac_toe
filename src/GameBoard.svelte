<script>
  import { createEventDispatcher } from "svelte";
  import classnames from "classnames";
  import Nought from "./Nought.svelte";
  import Cross from "./Cross.svelte";

  const dispatch = createEventDispatcher();

  function makeMove(pos) {
    dispatch("makeMove", {
      pos: pos
    });
  }

  export let board;
  export let gameOver;
  export let winningLine;
  export let playables;
</script>

<div class="relative" style="padding-bottom: 100%">
  <div class="absolute board w-full h-full">
    {#each board as square, pos}
      <div
        on:click={() => makeMove(pos)}
        class={classnames(
          'border-4',
          'border-gray-400',
          'flex',
          'justify-center',
          'items-center',
          {
            'hover:border-green-400': playables[pos] && !gameOver,
            'hover:border-red-400': !playables[pos] && !gameOver,
            'border-yellow-400': winningLine.includes(pos)
          }
        )}>
        <div class="w-1/2" style="height: 50%">
          {#if square == 'X'}
            <Cross />
          {:else if square == 'O'}
            <Nought />
          {/if}
        </div>
      </div>
    {/each}
  </div>
</div>
