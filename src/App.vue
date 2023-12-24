<script setup>
import TheBarchart from "./components/TheBarchart.vue";
import TheBubblechart from "./components/TheBubblechart.vue";
import ThePiechart from "./components/ThePiechart.vue";
import TheDoughnutchart from "./components/TheDoughnutchart.vue";
import TheLinechart from "./components/TheLinechart.vue";
import ThePolarareachart from "./components/ThePolarareachart.vue";
import TheRadarchart from "./components/TheRadarchart.vue";
</script>
<template>
  <TheBarchart />
  <div class="gap"></div>
  <TheBubblechart />
  <div class="gap"></div>
  <ThePiechart />
  <div class="gap"></div>
  <TheDoughnutchart />
  <div class="gap"></div>
  <TheLinechart />
  <div class="gap"></div>
  <ThePolarareachart />
  <div class="gap"></div>
  <TheRadarchart />
</template>
<style scoped>
.gap {
  height: 1px;
  margin-bottom: 100px;
  border-bottom: 1px solid rgba(0, 0, 0, 0.24);
}
body{
  background-color: rgb(241 245 249);
}
</style>
