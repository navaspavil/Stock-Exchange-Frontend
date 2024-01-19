<template>
  <div class="container mx-auto p-4">
    <toast-component ref="toast"></toast-component>
    <StockSearch
      @search="handleSearch"
      @chart-type-selected="handleChartTypeChange"
    ></StockSearch>
    <CandlestickChart
      v-if="selectedChartType === 'candlestick' && candlestickData.length"
      :data="candlestickData"
      :key="chartKey"
    ></CandlestickChart>
    <LineChart
      v-if="selectedChartType === 'line' && lineChartData.length"
      :data="lineChartData"
      :key="chartKey"
    ></LineChart>
  </div>
</template>

<script>
import StockSearch from "./components/StockSearch.vue";
import CandlestickChart from "./components/CandlestickChart.vue";
import LineChart from "./components/LineChart.vue";
import ToastComponent from "./components/Toast.vue";
import axios from "axios";

export default {
  name: "App",
  components: {
    StockSearch,
    CandlestickChart,
    LineChart,
    ToastComponent,
  },
  data() {
    return {
      candlestickData: [],
      lineChartData: [],
      selectedChartType: "candlestick",
      chartKey: 0,
    };
  },
  async mounted() {
    const today = new Date();
    const startDate = new Date();
    startDate.setDate(startDate.getDate() - 200);

    await this.handleSearch(
      {
        symbol: "XYZ",
        startDate: startDate,
        endDate: today,
        period: "daily",
      },
      false
    );
  },
  methods: {
    handleChartTypeChange(selectedType) {
      this.selectedChartType = selectedType;
    },
    async handleSearch(searchParams, isClicked = true) {
      try {
        const response = await axios.get(
          `${process.env.VUE_APP_API_HOSTNAME}/api/search`,
          {
            params: searchParams,
          }
        );
        this.data = response.data.data.stockData;
        this.processData(response.data.data);
        if (isClicked) {
          this.$refs.toast.show("Data fetched successfully!", false);
        }
        this.chartKey++;
      } catch (error) {
        console.log({ error });
        this.$refs.toast.show(error.response.data.message, true);
      }
    },
    processData(apiData) {
      this.candlestickData = this.formatCandlestickData(apiData);
      this.lineChartData = this.formatLineChartData(apiData);
    },
    formatCandlestickData(apiData) {
      return apiData.stockData.map((item) => ({
        time: Math.floor(new Date(item.date).getTime() / 1000),
        open: Number(item.open),
        high: Number(item.high),
        low: Number(item.low),
        close: Number(item.close),
      }));
    },
    formatLineChartData(apiData) {
      return apiData.stockData.map((item) => ({
        time: Math.floor(new Date(item.date).getTime() / 1000),
        value: Number(item.close),
      }));
    },
  },
};
</script>
