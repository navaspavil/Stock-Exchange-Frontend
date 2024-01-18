<template>
  <div ref="chartContainer" class="chart-container"></div>
</template>

<script>
import { createChart } from "lightweight-charts";

export default {
  name: "LineChart",
  props: {
    data: {
      type: Array,
      required: true,
    },
  },
  mounted() {
    const chart = createChart(this.$refs.chartContainer);
    const lineSeries = chart.addLineSeries();
    lineSeries.setData(this.data);
  },
};
</script>

<style>
.chart-container {
  width: 100%;
  height: 300px;
}
</style>
