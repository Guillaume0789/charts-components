<template>
  <div class="gauge-container">
    <div v-if="props.invert" class="label">
      <span class="text" style="position: relative; top: calc(20% - 13px)">16 ha</span>
      <span class="text" style="position: relative; top: calc(34% - 13px)">12 ha</span>
      <span class="text" style="position: relative; top: calc(58% - 13px)">6 ha</span>
    </div>
    <div v-else class="label">
      <span class="text" style="position: relative; top: calc(25% - 13px)">15%</span>
      <span class="text" style="position: relative; top: calc(44% - 13px)">10%</span>
      <span class="text" style="position: relative; top: calc(64% - 13px)">5%</span>
    </div>
    <div
      class="bar-style"
      :style="
        props.invert
          ? 'flex-direction: column;'
          : 'flex-direction: column-reverse;'
      "
    >
      <!-- <div
        v-for="el in sections"
        :key="el"
        :style="
          'height: 25%; width: 100%;border : solid 1px; background-color :' +
          el.color +
          ';'
        "
      ></div> -->
      <div
        style="
          height: 25%;
          width: 100%;
          border: solid 1px;
          background-color: #e87163;
        "
        :style="props.invert ? 'height: 20%;' : 'height: 25%;'"
      ></div>
      <div
        style="
          height: 25%;
          width: 100%;
          border: solid 1px;
          background-color: #fff5cb;
        "
        :style="props.invert ? 'height: 20%;' : 'height: 25%;'"
      ></div>
      <div
        style="
          height: 25%;
          width: 100%;
          border: solid 1px;
          background-color: #c8e7a7;
        "
        :style="props.invert ? 'height: 30%;' : 'height: 25%;'"
      ></div>
      <div
        style="
          height: 25%;
          width: 100%;
          border: solid 1px;
          background-color: #00b050;
        "
        :style="props.invert ? 'height: 30%;' : 'height: 25%;'"
      ></div>
      <span class="dot" :style="'bottom: calc(' + percentResult + '% - 5px);'">
        <p v-if="props.invert">{{ props.value }} ha</p>
        <p v-else>{{ props.value }} %</p>
      </span>
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

const percentResult = computed(() => {
  let result = props.value * 5;

  if (result >= 100) {
    return 100;
  } else if (result <= 0) {
    return 0;
  } else {
    return result;
  }
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
  width: 200px;
  height: 450px;
  display: flex;
  justify-content: space-around;
}
.bar-style {
  height: 100%;
  width: 15%;
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
  width: 50px;
  position: absolute;
  top: -5px;
  left: 30px;
}
.label {
  width: 35%;
  display: flex;
  /* justify-content: space-evenly; */
  flex-direction: column;
}
.text {
  text-align: center;
  width: 100%;
  border: solid 1px;
}
</style>
