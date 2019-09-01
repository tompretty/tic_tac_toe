<script>
  import Nought from './Nought.svelte'
  import Cross from './Cross.svelte'

  export let scores
</script>

<div class="flex justify-around items-baseline">
  <div class="w-1/5">
    <Nought />
  </div>
  <div class="text-4xl text-gray-500">{scores.noughts} : {scores.crosses}</div>
  <div class="w-1/5">
    <Cross />
  </div>
</div>
