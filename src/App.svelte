<script lang="ts">  
  let ralValue = 0
  let result = 0

  const scaglioniIrpef = [
    {ralFrom: 0, ralTo: 15000, irpef: 23},
    {ralFrom: 15_001, ralTo: 28_000, irpef: 25},
    {ralFrom: 28_001, ralTo: 50_000, irpef: 35},
    {ralFrom: 50_001, ralTo: Infinity, irpef: 43}
  ]

  function calcolaNetto() {
    let r = 0

    for (const {irpef, ralFrom, ralTo} of scaglioniIrpef) {            
      if(ralValue > ralTo){ 
        r += (ralTo - ralFrom) * (100 - irpef)/100           
      }else{
        r += (ralValue - ralFrom) * (100 - irpef)/100
        break
      }
    }
    
    result = Math.ceil(r/13)
  }
</script>

<main>
  <h1>Calcolo RAL</h1>

  <div class="card">
    <label for="ralInput">Inserisci la RAL:</label>
    <input type="number" id="ralInput" bind:value={ralValue} />

    <button on:click={calcolaNetto}>CALCOLA RAL</button>

    {#if result > 0}
      <p>Il netto mensile (13 mensilità) è: {result} €</p>
    {/if}
  </div>

</main>

