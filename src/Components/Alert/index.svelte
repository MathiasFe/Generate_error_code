<script>
  import { Toaster, toast } from "svelte-sonner";
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();

  export let message = null;
  export let isSuccess = false;
  export let show = true;

  function changeFalseShow() {
    dispatch("changeShow");
  }

  $: if (show)
    if (isSuccess) {
      toast.success(message);
      changeFalseShow();
    } else toast.error(message);
</script>

<Toaster
  position="top-center"
  richColors
  theme="dark"
  visibleToasts={3}
  closeButton
  duration={2000}
/>
