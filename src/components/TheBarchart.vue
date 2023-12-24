<template>
  <section class="chart">
    <h1 class="chart__title" @click="test">Bar Chart</h1>
    <p class="text-center relative">
      A <span class="chart-main-word">bar chart</span> provides a way of showing
      data values represented as vertical bars. It is sometimes used to show
      trend data, and the comparison of multiple data sets side by side.
      <img
        src="../assets/Screenshot 2023-12-24 224340.png"
        alt=""
        class="ajab-sign"
      />
    </p>
    <div class="main-part">
      <div class="main-part__chart">
        <canvas ref="barchart_canvas"></canvas>
      </div>
      <div class="main-part__inputs">
        <transition-group class="each-controls" tag="div" name="list">
          <div class="controls" v-for="(item, i) in dummyArray" :key="i">
            <div class="control">
              <label for="first_data" class="control__label">Item : </label>
              <input
                type="text"
                class="control__input"
                id="first_data"
                v-model="data[i].first_data"
              />
            </div>
            <div class="control">
              <label for="second_data" class="control__label">Amount : </label>
              <input
                type="text"
                class="control__input"
                id="second_data"
                v-model.number="data[i].second_data"
              />
            </div>
          </div>
        </transition-group>
        <button class="btn btn--add-control" @click="addControl">
          <div class="plus-sign">+</div>
        </button>
      </div>
    </div>
    <button class="btn btn--create-chart" @click="createChart()">
      Create the Chart
    </button>
  </section>
</template>
<script setup>
import { ref, onMounted } from "vue";
import Chart from "chart.js/auto";
let currentChart;
const barchart_canvas = ref();
const dummyArray = ref([1, 1, 1]);
const data = ref(
  Array.from(Array(100), () => {
    return {
      first_data: null,
      second_data: null,
    };
  })
);
function addControl() {
  dummyArray.value.push(1);
}

function createChart(labels, data) {
  if (currentChart) currentChart.destroy();
  const fullArr = data.value.filter((item) => {
    if (!item.first_data || !item.second_data) return false;
    else return true;
  });
  currentChart = new Chart(barchart_canvas.value, {
    type: "bar",
    options: {
      responsive: true,
    },
    data: {
      labels: fullArr.map((row) => row.first_data),
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
          data: fullArr.map((row) => row.second_data),
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
  currentChart = new Chart(barchart_canvas.value, {
    type: "bar",
    options: {
      responsive: true,
    },
    data: {
      labels: ["Jan", "Feb", "March", "Apr", "May", "June", "Jul"],
      datasets: [
        {
          backgroundColor: ["rgba(54, 162, 235, 0.3)"],
          borderColor: "rgb(54, 162, 235)",
          borderWidth: 1,
          label: "My Chart",
          data: [65, 59, 80, 81, 56, 55, 40],
          animation: {
            duration: 2000,
          },
        },
      ],
    },
  });
});
</script>
