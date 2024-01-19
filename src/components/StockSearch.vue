<template>
  <div class="p-4">
    <h2 class="font-bold text-lg mb-6">Stock Data</h2>
    <div class="md:flex gap-4 justify-between">
      <div class="mb-4 md:mb-0 md:w-auto w-full">
        <label for="symbol" class="block text-gray-700 text-sm font-bold mb-2"
          >Symbol:</label
        >
        <input
          type="text"
          id="symbol"
          v-model="symbol"
          placeholder="Enter stock symbol"
          class="shadow appearance-none border w-full rounded-md py-2 px-4 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
        />
        <p v-if="errors.symbol" class="text-red-600 text-sm mt-1">
          {{ errors.symbol }}
        </p>
      </div>
      <div class="md:flex gap-4">
        <div class="mb-4 md:mb-0">
          <label
            for="start-date"
            class="block text-gray-700 text-sm font-bold mb-2"
            >Start Date:</label
          >
          <input
            type="date"
            id="start-date"
            v-model="startDate"
            class="shadow appearance-none border w-full md:w-auto rounded-md py-2 px-4 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
          />
          <p v-if="errors.startDate" class="text-red-600 text-sm mt-1">
            {{ errors.startDate }}
          </p>
        </div>
        <div class="mb-4 md:mb-0">
          <label
            for="end-date"
            class="block text-gray-700 text-sm font-bold mb-2"
            >End Date:</label
          >
          <input
            type="date"
            id="end-date"
            v-model="endDate"
            class="shadow w-full md:w-auto appearance-none border rounded-md py-2 px-4 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
          />
          <p v-if="errors.endDate" class="text-red-600 text-sm mt-1">
            {{ errors.endDate }}
          </p>
        </div>
        <div class="mb-6 md:mb-0">
          <label for="period" class="block text-gray-700 text-sm font-bold mb-2"
            >Period:</label
          >
          <select
            id="period"
            v-model="period"
            class="shadow border w-full md:w-auto rounded-md py-2 px-4 text-gray-700"
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
          class="w-full md:w-auto bg-blue-600 hover:bg-blue-700 text-white font-bold py-2 px-4 mt-auto rounded-md focus:outline-none focus:shadow-outline"
        >
          Search
        </button>
      </div>
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
  },
};
</script>
