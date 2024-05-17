<template>
  <div class="gauge-container">
    <div v-if="props.invert" class="label">
      <span class="text">16 ha</span>
      <span class="text">12 ha</span>
      <span class="text">6 ha</span>
    </div>
    <div v-else class="label">
      <span class="text">15%</span>
      <span class="text">10%</span>
      <span class="text">5%</span>
    </div>
    <div
      class="bar-style"
      :style="
        props.invert
          ? 'flex-direction: column;'
          : 'flex-direction: column-reverse;'
      "
    >
      <div
        v-for="el in sections"
        :key="el"
        :style="
          'height: 25%; width: 100%;border : solid 1px; background-color :' +
          el.color +
          ';'
        "
      ></div>
      <span class="dot" :style="'bottom: calc(' + props.value + '% - 5px);'">
        <p>11%</p></span
      >
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
  invert: Boolean,
});

const sections = ref([
  { id: 1, color: "#E87163" },
  { id: 2, color: "#FFF5CB" },
  { id: 3, color: "#C8E7A7" },
  { id: 4, color: "#00B050" },
]);
</script>
<style scoped>
.gauge-container {
  width: 150px;
  height: 450px;
  display: flex;
  justify-content: space-around;
}
.bar-style {
  height: 100%;
  width: 20%;
  position: relative;
  display: flex;
}
.dot {
  height: 10px;
  width: 10px;
  background-color: #000;
  border-radius: 50%;
  position: absolute;
  margin-left: calc(50% - 6px);
  z-index: 100;
}
.dot p {
  position: absolute;
  top: -5px;
  left: 30px;
}
.label {
  width: 60%;
  display: flex;
  justify-content: space-evenly;
  flex-direction: column;
}
.text {
  text-align: center;
  width: 100%;
  border: solid 1px;
}
</style>
