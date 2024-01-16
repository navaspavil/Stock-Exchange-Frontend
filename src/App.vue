<template>
  <div class="container mx-auto p-4">
    <StockSearch @search="handleSearch"></StockSearch>
    <StockDisplay v-if="data.length" :stockData="data"></StockDisplay>
  </div>
</template>

<script>
import StockSearch from "./components/StockSearch.vue";
import StockDisplay from "./components/StockDisplay.vue";
import axios from "axios";

export default {
  name: "App",
  components: {
    StockSearch,
    StockDisplay,
  },
  data() {
    return {
      data: [],
    };
  },
  methods: {
    async handleSearch(searchParams) {
      try {
        const response = await axios.get(`http://localhost:3000/api/search`, {
          params: searchParams,
        });
        this.data = response.data.data.stockData;
      } catch (error) {
        console.error("Error fetching stock data:", error);
        // Handle error
      }
    },
  },
};
</script>
