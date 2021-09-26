<script>
    import {createEventDispatcher} from 'svelte';

    const dispatch = createEventDispatcher();

    export let descricao;
    export let comprado;
</script>

<div>
  <label>
    <input type="checkbox" bind:checked={comprado} />
    {descricao}
  </label>
  <button on:click={() => dispatch("itemRemovido")}>Excluir</button>
</div>

<style>
    div {
        margin: 10px 0;
    }
</style>