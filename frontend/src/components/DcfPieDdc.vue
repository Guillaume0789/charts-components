<template>
<div>
  <div id="pie-chart"></div>
  <div
    
  >coucou</div>
</div>

</template>

<script setup>
import ApexCharts from "apexcharts";
import { ref, onMounted, computed, watch } from "vue";

/**
 * Variables & hydratation
 */

const props = defineProps({
  data: Array,
});

// Options utilisée par Apexcharts
const options = ref({
  series: props.data.serie,
  chart: {
    width: 380,
    height: 500,
    type: "pie",
  },
  title: {
    text: "SDC 1",
    margin: 0,
    align: 'center',
    style: {
      fontSize:  '20px',
    },
  },
  labels: props.data.labels,
  legend: {
    show: false,
    position: 'left',
  }
});

const chart = ref(null);

/**
 * Cycle de vie du composant
 */

onMounted(() => {
  chart.value = new ApexCharts(document.getElementById("pie-chart"), options.value);
  chart.value.render();
});

/**
 * Fonctions
 */

watch(
  () => props.serie,
  () => {
    options.value = {
      ...options.value,
      ...{
        series: props.serie,
      },
    };
    chart.value.updateOptions(options.value);
  }
);
</script>
