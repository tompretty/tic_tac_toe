<script>
  import Nought from "./Nought.svelte";
  import Cross from "./Cross.svelte";

  export let O;
  export let X;
</script>

<div class="flex items-baseline">
  <div class="w-1/3 flex justify-center">
    <div class="w-1/2">
      <Nought />
    </div>
  </div>
  <div class="w-1/3 flex justify-center text-4xl text-gray-500">{O} : {X}</div>
  <div class="w-1/3 flex justify-center">
    <div class="w-1/2">
      <Cross />
    </div>
  </div>
</div>
