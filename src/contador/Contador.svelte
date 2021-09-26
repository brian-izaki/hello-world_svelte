<script>
  let contador = 0;

  function increment() {
    contador++;
  }
</script>

<div>
  Valor: {contador}
  <button on:click={increment}>Incrementar</button>
  <button on:click={() => contador--}>Decrementar</button>
</div>

<style>
  button {
    background-color: blueviolet;
    color: white;
  }
</style>