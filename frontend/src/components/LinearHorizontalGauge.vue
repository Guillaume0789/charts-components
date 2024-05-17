<template>
  <div class="gauge-container">
    <div class="label" v-if="showLabel">
      <span class="text">3,5</span>
      <span class="text">4,25</span>
      <span class="text">5</span>
    </div>
    <div class="bar-style">
      <div
        v-for="el in sections"
        :key="el"
        :style="'height: 30px; width: 25%; background-color :' + el.color + ';'"
      ></div>
      <span class="dot" :style="'left:calc(' + props.value + '% - 5px);'"></span>
    </div>
  </div>
</template>

<script setup>
import ApexCharts from "apexcharts";
import { ref, onMounted, computed, watch } from "vue";

/**
 * Variables & hydratation
 */

const props = defineProps({
  value: Number,
  showLabel: Boolean
});

const sections = ref([
  { id: 1, color: "#E87163" },
  { id: 2, color: "#FFF5CB" },
  { id: 3, color: "#C8E7A7" },
  { id: 4, color: "#00B050" },
]);

</script>
<style scoped>
.gauge-container{
  width: 250px;
}
.bar-style {
  height: 30px;
  width: 100%;
  position: relative;
  display: flex;
}
.dot {
  height: 10px;
  width: 10px;
  background-color: #000;
  border-radius: 50%;
  position: absolute;
  top: calc(50% - 5px);
  z-index: 100;
}
.label{
  width: 100%;
  display: flex;
  justify-content: space-evenly;
}
.text{
  text-align: center;
  width: 30px;
}
</style>
