<script>
  // Properties
  export let data = [];
  export let year = 0;
  const continents = ["europe", "asia", "americas", "africa"];
  const options = [continents].concat(continents)
  export let selected = continents;
  let stop = true;
  let actions = ['Pause', 'Play']

  function reset(event) {
    stop = true;
    year = 0;
  }

  function animation(event) {
    stop = !stop;
    let interval = setInterval(() => {
        if (year < 214){
          if (stop){
            clearInterval(interval);
          } else {
            year += 1;
          }
        } else{
          reset(event);
          clearInterval(interval);
        }
      }, 25)
  }
  
  function pause(event) {
    stop = true;
  }

</script>

<div>
  <!-- slider -->
  <input type="range" min="0" max="214" bind:value={year} /><br/>
  Year: {year + 1800}<br/><br/>

  <!-- buttons -->
  <button on:click={animation}>{actions[+stop]}</button>
  <button on:click={reset}>Reset</button><br/><br/>

  <!-- dropdown menu -->
  <select bind:value={selected} on:change="{() => answer = ''}">
    {#each options as continent}
			<option value={continent}>
        {#if continent != continents}
          {continent}
        {/if}
			</option>
		{/each}
	</select>
</div>