<script>
    // Dimensions
    const width = 800;
    const height = 100;
    const margin = { top: 5, right: 5, bottom: 5, left: 5 };
    const innerWidth = width - margin.left - margin.right;
    const innerHeight = height - margin.top - margin.bottom;
  
    // Array
    const values = [2, 4, 6, 7, 9];

    import { scaleLog } from 'd3-scale';
    import { select }   from 'd3-selection';
    import { axisBottom }   from 'd3-axis';
    const scale = scaleLog().domain([1, 10]).range([0, innerWidth]);

    function xAxisBuilder(handle){
      const axis = axisBottom(scale);
      select(handle).call(axis);
    }
  </script>
  
  <svg viewBox="0 0 {width} {height}">
    <g transform="translate({margin.left},{margin.top})">
      {#each values as value}
        <circle cx={scale(value)} cy=31 r=10/>
        <text x={width/2} y='{height - 5}'> x-Axis </text>
      {/each}
    </g>
    <g transform="translate({margin.left},{innerHeight-20})"   use:xAxisBuilder> 
    </g> 
  </svg>

  <style>
    text {
      text-anchor: middle;
        font-size: small;
    }
  </style>
  