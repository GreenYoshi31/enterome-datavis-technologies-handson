<script>
    import { onMount } from "svelte";

    // Dimensions
    const width = 800;
    const height = 100;
    const margin = { top: 10, right: 20, bottom: 20, left: 20 };
    const innerWidth = width - margin.left - margin.right;
    const innerHeight = height - margin.top - margin.bottom;
  
    // Arrays
    const diff = 150
    const points = [
      innerWidth / 2 - 2 * diff,
      innerWidth / 2 - diff,
      innerWidth / 2,
      innerWidth / 2 + diff,
      innerWidth / 2 + 2 * diff
    ];
  
    // Color
    let color = "darkred";
    let opacity = null;

    // All lights with a higher index are on!
    let index = points.length;
    onMount(async () => {
      opacity = [.3, .3, .3, .3, .3]
      
      let interval = setInterval(function(){
        index -=1
        if(index > -1){
          opacity[4 - index] = 1;
        } else {
          color = "darkgreen";
          clearInterval(interval);
        }
      }, 1000)
    });
  </script>

  {#if !opacity}
    <svg viewBox="0 0 {width} {height}">
    <g transform="translate({margin.left},{margin.top})">
      {#each points as point, index}
        <circle cx={point} cy={margin.top + 30} r='40' fill={color} opacity={.3}/>
      {/each}
    </g>
  </svg>
{:else}
  <svg viewBox="0 0 {width} {height}">
    <g transform="translate({margin.left},{margin.top})">
      {#each points as point, index}
        <circle cx={point} cy={margin.top + 30} r='40' fill={color} opacity={opacity[index]}/>
      {/each}
    </g>
  </svg>
{/if}