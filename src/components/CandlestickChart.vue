<template>
  <div ref="chartContainer" class="chart-container"></div>
</template>

<script>
import { createChart } from "lightweight-charts";

export default {
  name: "CandlestickChart",
  props: {
    data: {
      type: Array,
      required: true,
    },
  },
  mounted() {
    const chart = createChart(this.$refs.chartContainer, {
      height: 300,
    });
    const candleSeries = chart.addCandlestickSeries({
      upColor: "#26a69a",
      downColor: "#ef5350",
      borderVisible: false,
      wickUpColor: "#26a69a",
      wickDownColor: "#ef5350",
    });
    candleSeries.setData(this.data);

    candleSeries.priceScale().applyOptions({
      autoScale: false,
      scaleMargins: {
        top: 0.1,
        bottom: 0.1,
      },
    });
  },
};
</script>

<style>
.chart-container {
  width: 100%;
  height: 300px;
}
</style>
