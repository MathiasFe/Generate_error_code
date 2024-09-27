<script>
  export let value = null;
  export let onChange = null;
  export let placeholder = null;
  export let readonly = false;
</script>

<input
  class="border rounded p-2 {readonly
    ? 'bg-gray-200 border-gray-200 focus:outline-none '
    : 'border-primary'}"
  {value}
  {placeholder}
  on:keyup={onChange}
  {readonly}
/>
