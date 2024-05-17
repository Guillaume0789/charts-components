<template>
  <v-container>
    <v-row class="my-8" justify="center">
      <PerfRadarChart :serie="data" />
    </v-row>
    <v-row class="my-8" justify="center">
      <LinearHorizontalGauge :value="50" :showLabel="false"/>
    </v-row>
    <v-row class="my-8" justify="center">
      <DcfPieDdc :data="data2" />
    </v-row>
    <v-row class="my-8" justify="center">
      <DcfPieDdc :data="data3" :showLegend="true"/>
    </v-row>
    <v-row class="my-8" justify="center">
      <LinearVerticalGauge :value="60" :invert="false" class="mx-5"/>
      <LinearVerticalGauge :value="50" :invert="true"/>
    </v-row>
  </v-container>
</template>

<script setup>
import { ref, onMounted, computed, watch } from "vue";

const data = ref([3, 2, 1.5, 3, 2.3, 3]);
const data2 = ref(
  {
    title: "SDC 1",
    serie : [1.6, 2, 2.5, 1, 4],
    labels : ["Culture 1", "Culture 2", "Culture 3", "Culture 4", "Culture 5"]
  }
);
const data3 = ref(
  {
    title: "SAU",
    serie : [1.6, 2, 2.5, 1, 4],
    labels : ["Culture 1", "Culture 2", "Culture 3", "Culture 4", "Culture 5"]
  }
);
</script>
