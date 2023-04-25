<script>
  // D3 stuff
  import { csv, scaleLinear, scaleTime, format, extent, timeFormat } from "d3";
    export let dataset
  // Components
  import AxisBottom from "./shared/AxisBottom.svelte";
  import AxisLeft from "./shared/AxisLeft.svelte";
  import Marks from "./shared/Marks.svelte";
  export let graphConfiguration;
  
  const innerHeight =
      graphConfiguration.Dimensions.height -
      graphConfiguration.Margin.top -
      graphConfiguration.Margin.bottom,
    innerWidth =
      graphConfiguration.Dimensions.width -
      graphConfiguration.Margin.left -
      graphConfiguration.Margin.right;

  const tickFormat = (value) => timeFormat("%a")(value);

  $: xScale = scaleTime()
    .domain(extent(dataset, (d) => d.timestamp))
    .range([0, innerWidth])
    .nice();

  $: yScale = scaleLinear()
    .domain(extent(dataset, (d) => d.temperature))
    .range([innerHeight, 0])
    .nice();

  const xAxisLabel = "Time",
    yAxisLabel = "Temperature";
</script>

<main>
  <h1>Temperature vs Time</h1>
  <svg
    width={graphConfiguration.Dimensions.width}
    height={graphConfiguration.Dimensions.height}
  >
    <g
      transform={`translate(${graphConfiguration.Margin.left},${graphConfiguration.Margin.top})`}
    >
      <AxisBottom {xScale} {innerHeight} {tickFormat} />
      <text transform={`translate(${-100},${innerHeight / 2}) rotate(-90)`}
        >{yAxisLabel}</text
      >
      <AxisLeft {yScale} {innerWidth} />
      <text x={innerWidth / 2} y={innerHeight + 50}>{xAxisLabel}</text>
      <Marks {dataset} {xScale} {yScale} />
    </g>
  </svg>
  
</main>

<style>
  h1,
  main {
    margin-left: 500px;
  }
  text {
    text-anchor: middle;
    font-size: 2em;
    fill: rgb(71, 68, 65);
  }
  svg {
    display: block;
    position: absolute;
  }
</style>
