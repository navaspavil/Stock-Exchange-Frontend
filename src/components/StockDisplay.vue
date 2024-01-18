<template>
  <div class="p-4">
    <h2 class="text-xl font-bold mb-4">Stock Data</h2>
    <table class="table-auto w-full">
      <thead>
        <tr class="bg-gray-200">
          <th class="px-4 py-2">Date</th>
          <th class="px-4 py-2">Open</th>
          <th class="px-4 py-2">High</th>
          <th class="px-4 py-2">Low</th>
          <th class="px-4 py-2">Close</th>
          <th class="px-4 py-2">Volume</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in stockData" :key="item.date" class="bg-white">
          <td class="border px-4 py-2">{{ item.date }}</td>
          <td class="border px-4 py-2">{{ item.open }}</td>
          <td class="border px-4 py-2">{{ item.high }}</td>
          <td class="border px-4 py-2">{{ item.low }}</td>
          <td class="border px-4 py-2">{{ item.close }}</td>
          <td class="border px-4 py-2">{{ item.volume }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "StockDisplay",
  props: {
    stockData: {
      type: Array,
      required: true,
    },
  },
};
</script>
