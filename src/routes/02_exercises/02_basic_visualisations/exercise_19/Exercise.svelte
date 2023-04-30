<script>
    // Dimensions
    const width = 800;
    const height = 400;
    const margin = { top: 20, right: 5, bottom: 5, left: 5 };
    const innerWidth = width - margin.left - margin.right;
    const innerHeight = height - margin.top - margin.bottom;
  
    // Array
    const values = [
      { x: 2, y: 1, category: "cat1" },
      { x: 4, y: 2, category: "cat3" },
      { x: 6, y: 1, category: "cat2" },
      { x: 7, y: 3, category: "cat3" },
      { x: 9, y: 1, category: "cat2" }
    ];

    import { scaleLinear, scaleOrdinal } from 'd3-scale';
    import { schemeCategory10 } from 'd3-scale-chromatic';
    import { axisBottom } from 'd3-axis';
    import { select }   from 'd3-selection';

    const scalex = scaleLinear().domain([0, 10]).range([0, innerWidth]);
    const scaley = scaleLinear().domain([0, 5]).range([0, innerHeight]);
    const uniques = [...new Set(values.map(v => v.category))]
    const scalec = scaleOrdinal(schemeCategory10).domain(uniques)

    function xAxisBuilder(handle){
      const axis = axisBottom(scalex);
      select(handle).call(axis);
    }

  </script>
  
  <svg viewBox="0 0 {width} {height}">
    <g transform="translate({margin.left},{margin.top})">
      {#each values as value}
        <circle cx={scalex(value.x)} cy={scaley(5 - value.y)} r=10 fill={scalec(value.category)}>
          <title>{value.category}</title>
        </circle>
        <text class='valueLabel' x={scalex(value.x)} y={scaley(5 - value.y) - 20}> {value.y} </text>
      {/each}
    </g>
    <g transform="translate({margin.left},{innerHeight + 9})" use:xAxisBuilder> 
    </g> 
  </svg>
  
  <style>
    text {
      text-anchor: middle;
      font-size: small;
    }
  </style>
  