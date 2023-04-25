<script>
	import { csv, scaleLinear, scaleTime, format, extent, timeFormat } from "d3";
	import LineChart from "./component/LineChart.svelte";
	import graphConfiguration from "./config/graph";
	let dataset = [];
	const row = (data) => {
    data.temperature = +data.temperature;
    data.timestamp = new Date(data.timestamp);
    return data;
  };
	csv("data/temperature.csv", row).then((data) => (dataset = data));
  </script>
  <section>
  <LineChart {graphConfiguration} dataset={dataset}/>
 
</section>