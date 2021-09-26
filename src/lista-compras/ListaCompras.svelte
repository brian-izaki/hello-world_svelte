<script>
  import ListaItem from './ListaItem.svelte';


  let itens = JSON.parse(localStorage.getItem("itens")) || [];

  let item = {
    comprado: false,
    descricao: '',
  };

  // variável reativa, se fosse let ele não iria alterar
  $: itensPendentes = itens.filter((item) => !item.comprado).length

  $: {
    localStorage.setItem("itens", JSON.stringify(itens))
  }

  function saveItem() {    
    if (item.descricao)
      itens = [
        ...itens,
        {
          comprado: item.comprado,
          descricao: item.descricao,
        },
      ];
    item.descricao = '';
  }

  function removerItem(item) {
    itens = itens.filter(i => i !== item)
  }
</script>

<section>
  <h1>Lista de compras</h1>

  <form on:submit|preventDefault={saveItem}>
    <input bind:value={item.descricao} type="text" name="item" />
    <button type="submit">Adicionar</button>
  </form>

  {#if itens.length === 0}
    <div style="margin: 20px;">A lista está vazia</div>
  {:else}
    {#each itens as item, index}
      <ListaItem
        bind:comprado={item.comprado}
        descricao={item.descricao}
        on:itemRemovido={() => removerItem(item)}
      />
    {/each}
  {/if}

  <div>Itens pendentes: {itensPendentes}</div>
</section>
