<template>
  <div id="radar-chart"></div>
</template>

<script setup>
import ApexCharts from "apexcharts";
import { ref, onMounted, computed, watch } from "vue";

/**
 * Variables & hydratation
 */

const props = defineProps({
  serie: Array,
});

// Options utilisée par Apexcharts
const options = ref({
  series: [
    {
      name: "Series 1",
      data: props.serie,
    },
  ],
  chart: {
    type: "radar",
    height: 400,
    width: 700,
    toolbar: {
      show: false,
    },
  },
  plotOptions: {
    radar: {
      size: 140,
      polygons: {
        strokeWidth: 0.5,
        fill: {
          colors: ["#92D050", "#FFEC98", "#C00000", "#C00000"],
        },
      },
    },
  },
  legend: {
    show: false,
  },
  markers: {
    size: 0,
  },
  fill: {
    opacity: 0,
  },
  stroke: {
    width: 3,
    colors: ["black"],
  },
  yaxis: {
    stepSize: 1,
    min: 0,
    max: 4,
    labels: {
      offsetX: 0,
      offsetY: 20,
      style: {
        fontSize: "18px",
        fontWeight: 600,
      },
    },
  },
  xaxis: {
    categories: [
      "Durée de couverture du sol",
      "Indice de Diversité Cultivée",
      "Carbone humifié restitué",
      "Balance Global Azotée",
      "Autonomie Azotée",
      "Accueil de la biodiversité",
      "IFT",
    ],
    labels: {
      offsetX: 0,
      offsetY: 0,
      style: {
        colors: ["#000", "#000", "#000", "#000", "#000", "#000"],
        fontSize: "15px",
        fontWeight: 500,
      },
    },
  },
});

const chart = ref(null);

/**
 * Cycle de vie du composant
 */

onMounted(() => {
  chart.value = new ApexCharts(document.getElementById("radar-chart"), options.value);
  chart.value.render();
});

/**
 * Fonctions
 */

// watch (() => props.data, () => {
//   options.value = {
//     ...options.value,
//     ...{
//       series: props.data,
//     }
//   }
//   chart.value.updateOptions(options.value);
// })
</script>
