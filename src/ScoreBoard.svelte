<script>
  import Nought from "./Nought.svelte";
  import Cross from "./Cross.svelte";

  export let O;
  export let X;
</script>

<div class="flex justify-around items-baseline">
  <div class="w-1/5">
    <Nought />
  </div>
  <div class="text-4xl text-gray-500">{O} : {X}</div>
  <div class="w-1/5">
    <Cross />
  </div>
</div>
