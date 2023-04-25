<script>
    export let yScale;
    export let innerWidth;
  </script>
  
  {#each yScale.ticks() as tick, i}
    <g transform={`translate(0,${yScale(tick)})`}>
      <line x1={0} x2={innerWidth} />
      <text x="-3" y={yScale(tick)} dy="0.32em">{tick}</text>
    </g>
  {/each}
  
  <style>
    text {
      text-anchor: end;
      fill: rgb(0, 0, 0);
      font-family: "Montserrat", sans-serif;
    }
    line {
      stroke: #525250;
    }
  </style>
  