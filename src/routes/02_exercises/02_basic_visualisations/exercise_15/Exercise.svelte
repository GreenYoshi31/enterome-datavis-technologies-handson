<script>
    const width = 100;
    const height = 100;
    const margin = { top: 5, right: 5, bottom: 5, left: 5 };
    const innerWidth = width - margin.left - margin.right;
    const innerHeight = height - margin.top - margin.bottom;

    const w = 40;
    const h = 40;
    const x1 = (innerWidth - w) / 2 - 1;
    const y1 = (innerHeight - h) / 2 - 1;

    const radius = 20;
    const cx1 = (innerWidth + w) / 2 - 1;
    const cy1 = (innerHeight + h) / 2 - 1;
  </script>
  
  <svg {width} {height}>
    <g transform="translate({margin.left}, {margin.top})">
      <rect x={x1} y={y1} width={w} height={h} fill='yellow' />
      <circle cx={cx1} cy={cy1} r={radius} fill='skyblue' />
    </g>
  </svg>
  
  <style>
    svg {
      border: 1px solid black;
      border-radius: 5px;
    }
  </style>
  