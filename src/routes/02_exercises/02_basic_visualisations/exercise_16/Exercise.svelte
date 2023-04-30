<script>
    const width = 100;
    const height = 100;
    const margin = { top: 5, right: 5, bottom: 5, left: 5 };
    const innerWidth = width - margin.left - margin.right;
    const innerHeight = height - margin.top - margin.bottom;
    const radius = Math.min(width, height) / 5
  </script>
  
  <svg viewbox = '0 0 {width} {height}'>
    <g transform="translate({margin.left}, {margin.top})">
      <circle cx={innerWidth / 2} cy={innerHeight / 2} r={radius} fill="teal" />
    </g>
  </svg>
  
  <style>
  svg {
    border: 1px solid black;
      border-radius: 5px;
  }
  </style>