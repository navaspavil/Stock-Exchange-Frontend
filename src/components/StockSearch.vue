<template>
  <div class="p-4">
    <h2 class="font-bold text-lg mb-6">
      {{ symbol === "" ? "XYZ" : "" }} Stock Data
    </h2>
    <div class="flex gap-4 justify-between">
      <div>
        <label for="symbol" class="block text-gray-700 text-sm font-bold mb-2"
          >Symbol:</label
        >
        <input
          type="text"
          id="symbol"
          v-model="symbol"
          placeholder="Enter stock symbol"
          class="shadow appearance-none border rounded-md py-2 px-4 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
        />
        <p v-if="errors.symbol" class="text-red-600 text-sm mt-1">
          {{ errors.symbol }}
        </p>
      </div>
      <div class="flex gap-4">
        <div>
          <label
            for="start-date"
            class="block text-gray-700 text-sm font-bold mb-2"
            >Start Date:</label
          >
          <input
            type="date"
            id="start-date"
            v-model="startDate"
            class="shadow appearance-none border rounded-md py-2 px-4 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
          />
          <p v-if="errors.startDate" class="text-red-600 text-sm mt-1">
            {{ errors.startDate }}
          </p>
        </div>
        <div>
          <label
            for="end-date"
            class="block text-gray-700 text-sm font-bold mb-2"
            >End Date:</label
          >
          <input
            type="date"
            id="end-date"
            v-model="endDate"
            class="shadow appearance-none border rounded-md py-2 px-4 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
          />
          <p v-if="errors.endDate" class="text-red-600 text-sm mt-1">
            {{ errors.endDate }}
          </p>
        </div>
        <div>
          <label for="period" class="block text-gray-700 text-sm font-bold mb-2"
            >Period:</label
          >
          <select
            id="period"
            v-model="period"
            class="shadow border rounded-md py-2 px-4 text-gray-700"
          >
            <option value="daily">Daily</option>
            <option value="hourly">Hourly</option>
          </select>
        </div>
        <button
          @click="fetchStockData"
          :class="{
            'mb-6': errors.startDate || errors.endDate || errors.symbol,
          }"
          class="bg-blue-600 hover:bg-blue-700 text-white font-bold py-2 px-4 mt-auto rounded-md focus:outline-none focus:shadow-outline"
        >
          Search
        </button>
      </div>
    </div>

    <div class="w-full">
      <select
        id="chartType"
        v-model="selectedChartType"
        @change="selectChartType"
        class="shadow border rounded-md py-2 px-3 text-gray-700 mt-16 mb-10 float-right"
      >
        <option value="candlestick">Candlestick Chart</option>
        <option value="line">Line Chart</option>
      </select>
    </div>
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
      selectedChartType: "candlestick",
      errors: {
        symbol: "",
        startDate: "",
        endDate: "",
      },
    };
  },
  methods: {
    validateInput() {
      this.resetErrors();

      if (!this.symbol) {
        this.errors.symbol = "Symbol is required";
      }

      if (!this.startDate) {
        this.errors.startDate = "Start date is required";
      }

      if (!this.endDate) {
        this.errors.endDate = "End date is required";
      } else if (
        this.startDate &&
        new Date(this.startDate) > new Date(this.endDate)
      ) {
        this.errors.endDate = "End date must be after start date";
      }

      return Object.values(this.errors).every((error) => !error);
    },

    resetErrors() {
      this.errors.symbol = "";
      this.errors.startDate = "";
      this.errors.endDate = "";
    },

    fetchStockData() {
      if (this.validateInput()) {
        this.$emit("search", {
          symbol: this.symbol,
          startDate: this.startDate,
          endDate: this.endDate,
          period: this.period,
        });
      }
    },
    selectChartType() {
      this.$emit("chart-type-selected", this.selectedChartType);
    },
  },
};
</script>
