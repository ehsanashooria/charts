<template>
  <section class="chart">
    <h1 class="chart__title" @click="test">Line Chart</h1>
    <p class="text-center">
      A <span class="chart-main-word">line chart</span> is a way of plotting
      data points on a line. Often, it is used to show trend data, or the
      comparison of two data sets.
      <img
        src="../assets/Screenshot 2023-12-24 224340.png"
        alt=""
        class="ajab-sign"
      />
    </p>
    <div class="main-part">
      <div class="main-part__chart">
        <canvas ref="line_canvas" class="canvas"></canvas>
      </div>
      <div class="main-part__inputs">
        <transition-group class="each-controls" tag="div" name="list">
          <div class="controls" v-for="(item, i) in dummyArray" :key="i">
            <div class="control">
              <label for="x" class="control__label">Item : </label>
              <input
                type="text"
                class="control__input"
                id="x"
                v-model="data[i].item"
              />
            </div>
            <div class="control">
              <label for="y" class="control__label">Amount(1) : </label>
              <input
                type="text"
                class="control__input"
                id="y"
                v-model="data[i].amount1"
              />
            </div>
            <div class="control">
              <label for="y" class="control__label">Amount(2) : </label>
              <input
                type="text"
                class="control__input"
                id="y"
                v-model="data[i].amount2"
              />
            </div>
          </div>
        </transition-group>
        <button class="btn btn--add-control" @click="addControl">
          <div class="plus-sign">+</div>
        </button>
      </div>
    </div>
    <button class="btn btn--create-chart" @click="createChart">
      Create the Chart
    </button>
  </section>
</template>
<script setup>
import { ref, onMounted } from "vue";
import Chart from "chart.js/auto";
let currentChart;
const line_canvas = ref();
const dummyArray = ref([1, 1, 1]);
const data = ref(
  Array.from(Array(100), () => {
    return {
      item: null,
      amount1: null,
      amount2: null,
    };
  })
);
function addControl() {
  dummyArray.value.push(1);
}

function createChart() {
  if (currentChart) currentChart.destroy();
  const fullArr = data.value.filter((item) => {
    if (!item.item || !item.amount1 || !item.amount2) return false;
    else return true;
  });
  currentChart = new Chart(line_canvas.value, {
    type: "line",
    options: {},
    data: {
      labels: fullArr.map((item) => item.item),
      datasets: [
        {
          label: "First Dataset",
          data: fullArr.map((item) => item.amount1),
          full: false,
          borderColor: "rgb(75, 192, 192)",
          tension: 0.1,
          animation: {
            duration: 2000,
          },
        },
        {
          label: "Second Dataset",
          data: fullArr.map((item) => item.amount2),
          full: false,
          borderColor: "rgb(239 68 68)",
          tension: 0.1,
          animation: {
            duration: 2000,
          },
        },
      ],
    },
  });
}

onMounted(() => {
  Chart.defaults.font.family = "Estedad";
  currentChart = new Chart(line_canvas.value, {
    type: "line",
    options: {},
    data: {
      labels: ["Jan", "Feb", "March", "Apr", "May", "June", "Jul"],
      datasets: [
        {
          label: "My Chart",
          data: [65, 59, 80, 81, 56, 55, 40],
          full: false,
          borderColor: "rgb(75, 192, 192)",
          tension: 0.1,
          animation: {
            duration: 2000,
          },
        },
      ],
    },
  });
});
</script>
<style scoped></style>
