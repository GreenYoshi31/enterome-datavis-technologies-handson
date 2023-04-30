<script>
    // Dimensions
    const width = 600;
    const height = 300;
    const margin = { top: 10, right: 10, bottom: 30, left: 60 };
    const innerWidth = width - margin.left - margin.right;
    const innerHeight = height - margin.top - margin.bottom;
  
    // Array
    const data = [
      { service: "Netflix", viewers: 2.9 },
      { service: "Amazon Prime Video", viewers: 1.3 },
      { service: "Disney+", viewers: 2.1 },
      { service: "Hulu", viewers: 0.9 },
      { service: "Apple TV", viewers: 1.1 },
      { service: "Rakuten", viewers: 0.4 }
    ];

    import { scaleLinear, scaleBand } from 'd3-scale';
    import { axisBottom, axisLeft } from 'd3-axis';
    import { select }   from 'd3-selection';
    const scaley = scaleLinear().domain([3, 0]).range([0, innerHeight]);
    const uniques = [...new Set(data.map(v => v.service))]
    const scalex = scaleBand().domain(uniques).range([0,innerWidth])

    function yAxisBuilder(handle){
      const axisy = axisLeft(scaley);
      select(handle).call(axisy);
    }

    function xAxisBuilder(handle){
      const axisx = axisBottom(scalex);
      select(handle).call(axisx);
    }
  </script>
  
  <!-- setting a viewBox and max-width allows the SVG to shrink but not grow! -->
  <svg viewbox="0 0 {width} {height}" style="max-width: {width}px">
    <g transform={`translate(${margin.left},${margin.top})`}>
      {#each data as platform}
        <rect x={scalex(platform.service) + 34} y={innerHeight - scaley(3 - platform.viewers)} width={21} height={scaley(3 - platform.viewers)} fill='#ff00bf' />
      {/each}
    </g>
    <g transform="translate({margin.left - 10},{margin.top})" use:yAxisBuilder> 
    </g>
    <g transform="translate({margin.left},{innerHeight + 20})" use:xAxisBuilder> 
    </g>
  </svg>