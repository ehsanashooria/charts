<template>
  <section class="chart">
    <h1 class="chart__title" @click="test">Doughnut Chart</h1>
    <p class="text-center">
      Pie and <span class="chart-main-word">doughnut</span> charts are probably
      the most commonly used charts. They are divided into segments, the arc of
      each segment shows the proportional value of each piece of data.
      <img
        src="../assets/Screenshot 2023-12-24 224340.png"
        alt=""
        class="ajab-sign"
      />
    </p>
    <div class="main-part">
      <div class="main-part__chart">
        <canvas ref="doughnutchart_canvas" class="canvas"></canvas>
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
              <label for="y" class="control__label">Amount : </label>
              <input
                type="text"
                class="control__input"
                id="y"
                v-model="data[i].amount"
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
const doughnutchart_canvas = ref();
const dummyArray = ref([1, 1, 1]);
const data = ref(
  Array.from(Array(100), () => {
    return {
      item: null,
      amount: null,
    };
  })
);
function addControl() {
  dummyArray.value.push(1);
}

function createChart() {
  if (currentChart) currentChart.destroy();
  const fullArr = data.value.filter((item) => {
    if (!item.item || !item.amount) return false;
    else return true;
  });
  currentChart = new Chart(doughnutchart_canvas.value, {
    type: "doughnut",
    options: {},
    data: {
      labels: fullArr.map((item) => item.item),
      datasets: [
        {
          backgroundColor: [
            "rgba(255, 99, 132, 0.8)",
            "rgba(54, 162, 235, 0.8)",
            "rgba(255, 159, 64, 0.8)",
            "rgba(153, 102, 255, 0.8)",
            "rgba(255, 205, 86, 0.8)",
            "rgba(75, 192, 192, 0.8)",
            "rgba(201, 203, 207, 0.8)",
          ],
          label: "My Chart",
          data: fullArr.map((item) => item.amount),
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
  currentChart = new Chart(doughnutchart_canvas.value, {
    type: "doughnut",
    options: {},
    data: {
      labels: ["Red", "Blue", "Yellow"],
      datasets: [
        {
          backgroundColor: [
            "rgb(255, 99, 132)",
            "rgb(54, 162, 235)",
            "rgb(255, 205, 86)",
          ],
          label: "My Chart",
          data: [300, 50, 100],
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
