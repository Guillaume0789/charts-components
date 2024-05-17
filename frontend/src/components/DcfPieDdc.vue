<template>
  <div
    class="pie-container"
    :style="
      props.showLegend
        ? 'align-items: end; width: 600px;'
        : 'align-items: center;'
    "
  >
    <div :id="props.data.title"></div>
    <LinearHorizontalGauge
      :value="78"
      :showLabel="true"
      :style="props.showLegend ? 'margin-right: 60px' : ''"
    />
  </div>
</template>

<script setup>
import ApexCharts from "apexcharts";
import { ref, onMounted, computed, watch } from "vue";

/**
 * Variables & hydratation
 */

const props = defineProps({
  data: Object,
  showLegend: Boolean,
});

// Options utilisée par Apexcharts
const options = ref({
  series: props.data.serie,
  chart: {
    width: props.showLegend ? 600 : 300,
    type: "pie",
    toolbar: {
      show: false,
    },
    animations: {
        enabled: false,
    }
  },
  title: {
    text: props.data.title,
    align: "center",
    style: {
      fontSize: "20px",
    },
  },
  labels: props.data.labels,
  legend: {
    show: props.showLegend,
    width: 200,
    fontSize: "20px",
    position: "left",
    markers: {
      width: 30,
      height: 20,
      radius: 0,
    },
  },
  plotOptions: {
    pie: {
      size: "200px",
    },
  },
});

const chart = ref(null);

/**
 * Cycle de vie du composant
 */

onMounted(() => {
  chart.value = new ApexCharts(
    document.getElementById(props.data.title),
    options.value
  );
  chart.value.render();
});
</script>
<style scoped>
.pie-container {
  display: flex;
  flex-direction: column;
}
.apexcharts-legend.apx-legend-position-bottom.apexcharts-align-left,
.apexcharts-legend.apx-legend-position-top.apexcharts-align-left,
.apexcharts-legend.apx-legend-position-right,
.apexcharts-legend.apx-legend-position-left {
  justify-content: center !important;
}
</style>
