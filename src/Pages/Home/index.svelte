<script>
  import Field from "../../Components/fields/index.svelte";
  import Button from "../../Components/Buttons/index.svelte";
  import Alert from "../../Components/Alert/index.svelte";

  export let title = null;

  let sigla = null;
  let result = null;
  let show = false;
  let message = "";
  let isSuccess = false;
  let setTimeId = 0;

  const handlerChangeSigla = (event) => {
    event.preventDefault();
    sigla = event?.target?.value ?? "";
  };

  const generateCode = (event) => {
    event.preventDefault();
    const value = Math.random().toString(36).substring(2, 6).toUpperCase();
    if (sigla) result = sigla + value;
    else result = value;

    copy(result);
  };

  const changeShow = () => {
    show = !show;
  };

  const copy = (value) => {
    if (setTimeId > 0) clearInterval(setTimeId);
    show = false;

    navigator.clipboard.writeText(`${value}`).catch((error) => {
      message = error;
      changeShow();
      isSuccess = false;
    });
    message = `Codigo ${result} copiado para sua área de transferencia`;
    changeShow();
    isSuccess = true;

    setTimeId = setTimeout(() => {
      show = false;
    }, 2000);
  };
</script>

<Alert on:changeShow={changeShow} {message} {isSuccess} {show} />

<div class="border rounded border-primary p-4">
  {#if title}
    <h4 class="text-center text-gray-200">{title}</h4>
  {/if}
  <form class="flex flex-col justify-center items-center gap-2 mt-2">
    <Field
      value={sigla}
      onChange={handlerChangeSigla}
      placeholder="Insira a sigla inicial"
    />

    <Button label="Gerar código" onClick={generateCode} />

    <Field
      value={result}
      placeholder="O codigo aparecerá aqui"
      readonly={true}
    />
  </form>
</div>
