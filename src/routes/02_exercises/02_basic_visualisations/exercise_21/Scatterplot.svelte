<script>
  // Dimensions
  const [height, width] = [400, 600];
  const margin = { top: 50, right: 5, bottom: 55, left: 50 };
  const innerWidth = width - margin.left - margin.right;
  const innerHeight = height - margin.top - margin.bottom;

  export let data = null;

  const life_exp = (data.countries.map(o => +o.life_exp));
  const income = (data.countries.map(o => +o.income));
  const population = (data.countries.map(o => +o.population));
  const continents = [...new Set(data.countries.map(v => v.continent))]

  import { scaleLinear, scalePow, scaleOrdinal } from 'd3-scale';
  import { schemeCategory10 } from 'd3-scale-chromatic';
  import { axisBottom, axisLeft } from 'd3-axis';
  import { select }   from 'd3-selection';

  const scaley = scaleLinear().domain([50, 0]).range([0, innerHeight]);
  const scalex = scaleLinear().domain([0, 5000]).range([0,innerWidth]);
  const scaler = scalePow().exponent(.2).domain([0, 350000000]).range([0,10])
  const scalec = scaleOrdinal(schemeCategory10).domain(continents)

  function yAxisBuilder(handle){
    const axisy = axisLeft(scaley);
    select(handle).call(axisy);
  }

    function xAxisBuilder(handle){
      const axisx = axisBottom(scalex);
      select(handle).call(axisx);
    }

</script>
  
<svg viewBox="0 0 {width} {height}" style="max-width: {width}px">
  {#each data.countries as country}
    <g transform="translate({margin.left}, {margin.top})">
        <circle cx={scalex(+country.income)} cy={scaley(+country.life_exp)} r={scaler(+country.population)} fill={scalec(country.continent)}>;
        <title>{country.country}</title>;
    </g>
  {/each}
  <g transform="translate({margin.left - 20},{margin.top})" use:yAxisBuilder> 
  </g>
  <g transform="translate({margin.left},{innerHeight + margin.top + 20})" use:xAxisBuilder> 
  </g>
  <text class="title" x={width/ 2} y={margin.top - 10} text-anchor='middle' font-size='2.25em'>Gapminder Scatterplot</text>
 </svg>
  