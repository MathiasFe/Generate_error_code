<script>
  export let label = null;
  export let onClick = null;
</script>

<button
  class="border border-gray-200 p-2 w-full rounded-md text-gray-200 hover:bg-gray-200 hover:text-[#3C3C3C] transition-all duration-400 ease-in-out"
  on:click={onClick}>{label}</button
>
