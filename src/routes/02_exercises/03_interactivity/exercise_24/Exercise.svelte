<script>
  import { json } from "d3-fetch";
  import { onMount } from "svelte";

  import Controls from "./Controls.svelte";
  import Scatterplot from "./Scatterplot.svelte";

  // Load the data
  let data = null;
  onMount(async () => {
    data = await json("/data/gapminder.json");
  });

  let year = 0;
  let selected = ["europe", "asia", "americas", "africa"];
</script>

{#if !data}
  <p>Loading the data, please wait...</p>
{:else}
  <div>
    <Scatterplot data={data[year]['countries'].filter(d => selected.includes(d.continent))} />
    <Controls {data} bind:year bind:selected/>
  </div>
{/if}
