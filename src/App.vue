<template>
  <div id="app">
    <waterBillsChart :water-bills="waterBillsData" />
  </div>
</template>

<script>
import waterBillsChart from "./components/waterBillsChart.vue";
import { data } from "./databaseWaterBills";

export default {
  name: "App",
  components: {
    waterBillsChart,
  },
  data() {
    return {
      waterBillsData: data,
    };
  },
};
</script>
