<template>
  <div class="p-4">
    <div class="mb-4">
      <label for="symbol" class="block text-gray-700 text-sm font-bold mb-2"
        >Symbol:</label
      >
      <input
        type="text"
        id="symbol"
        v-model="symbol"
        placeholder="Enter stock symbol"
        class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
      />
    </div>
    <div class="mb-4">
      <label for="start-date" class="block text-gray-700 text-sm font-bold mb-2"
        >Start Date:</label
      >
      <input
        type="date"
        id="start-date"
        v-model="startDate"
        class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
      />
    </div>
    <div class="mb-4">
      <label for="end-date" class="block text-gray-700 text-sm font-bold mb-2"
        >End Date:</label
      >
      <input
        type="date"
        id="end-date"
        v-model="endDate"
        class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
      />
    </div>
    <div class="mb-4">
      <label for="period" class="block text-gray-700 text-sm font-bold mb-2"
        >Period:</label
      >
      <select
        id="period"
        v-model="period"
        class="shadow border rounded w-full py-2 px-3 text-gray-700 mb-3"
      >
        <option value="daily">Daily</option>
        <option value="hourly">Hourly</option>
      </select>
    </div>
    <button
      @click="fetchStockData"
      class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
    >
      Search
    </button>
  </div>
</template>

<script>
export default {
  name: "StockSearch",
  data() {
    return {
      symbol: "",
      startDate: "",
      endDate: "",
      period: "daily",
    };
  },
  methods: {
    fetchStockData() {
      // Emit an event with the search parameters
      this.$emit("search", {
        symbol: this.symbol,
        startDate: this.startDate,
        endDate: this.endDate,
        period: this.period,
      });
    },
  },
};
</script>
