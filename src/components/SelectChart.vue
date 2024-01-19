<template>
  <div class="w-full">
    <select
      id="chartType"
      v-model="selectedChartType"
      @change="selectChartType"
      class="shadow border rounded-md py-2 px-3 text-gray-700 mb-10 float-right"
    >
      <option value="candlestick">Candlestick Chart</option>
      <option value="line">Line Chart</option>
    </select>
  </div>
</template>

<script>
export default {
  name: "SelectChart",
  data() {
    return {
      selectedChartType: "candlestick",
    };
  },
  methods: {
    selectChartType() {
      this.$emit("chart-type-selected", this.selectedChartType);
    },
  },
};
</script>
