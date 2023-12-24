<template>
  <section class="chart">
    <h1 class="chart__title" @click="test">Radar Chart</h1>
    <p class="text-center">
      A <span class="chart-main-word">radar chart</span> is a way of showing
      multiple data points and the variation between them. They are often useful
      for comparing the points of two or more different data sets.
      <img
        src="../assets/Screenshot 2023-12-24 224340.png"
        alt=""
        class="ajab-sign"
      />
    </p>
    <div class="main-part">
      <div class="main-part__chart">
        <canvas ref="radarchart_canvas"></canvas>
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
                v-model="data[i].label"
              />
            </div>
            <div class="control">
              <label for="second_data" class="control__label"
                >Amount(1) :
              </label>
              <input
                type="text"
                class="control__input"
                id="second_data"
                v-model.number="data[i].first_data"
              />
            </div>
            <div class="control">
              <label for="second_data" class="control__label"
                >Amount(2) :
              </label>
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
    <button class="btn btn--create-chart" @click="createChart">
      Create the Chart
    </button>
  </section>
</template>
<script setup>
import { ref, onMounted } from "vue";
import Chart from "chart.js/auto";
let currentChart;
const radarchart_canvas = ref();
const dummyArray = ref([1, 1, 1]);
const data = ref(
  Array.from(Array(100), () => {
    return {
      label: null,
      second_data: null,
      first_data: null,
    };
  })
);
function addControl() {
  dummyArray.value.push(1);
}

function createChart() {
  if (currentChart) currentChart.destroy();
  const fullArr = data.value.filter((item) => {
    if (!item.first_data || !item.second_data) return false;
    else return true;
  });
  currentChart = new Chart(radarchart_canvas.value, {
    type: "radar",
    options: {
      responsive: true,
      elements: {
        line: {
          borderWidth: 3,
        },
      },
    },
    data: {
      labels: fullArr.map((row) => row.label),
      datasets: [
        {
          label: "My First Dataset",
          fill: true,
          data: fullArr.map((row) => row.first_data),
          backgroundColor: "rgba(255, 99, 132, 0.2)",
          borderColor: "rgb(255, 99, 132)",
          pointBackgroundColor: "rgb(255, 99, 132)",
          pointBorderColor: "#fff",
          pointHoverBackgroundColor: "#fff",
          pointHoverBorderColor: "rgb(255, 99, 132)",
          animation: {
            duration: 2000,
          },
        },
        {
          label: "My Second Dataset",
          data: fullArr.map((row) => row.second_data),
          animation: {
            duration: 2000,
          },
          fill: true,
          backgroundColor: "rgba(54, 162, 235, 0.2)",
          borderColor: "rgb(54, 162, 235)",
          pointBackgroundColor: "rgb(54, 162, 235)",
          pointBorderColor: "#fff",
          pointHoverBackgroundColor: "#fff",
          pointHoverBorderColor: "rgb(54, 162, 235)",
        },
      ],
    },
  });
}

onMounted(() => {
  Chart.defaults.font.family = "Estedad";
  currentChart = new Chart(radarchart_canvas.value, {
    type: "radar",
    options: {
      responsive: true,
      elements: {
        line: {
          borderWidth: 3,
        },
      },
    },
    data: {
      labels: [
        "Eating",
        "Drinking",
        "Sleeping",
        "Designing",
        "Coding",
        "Cycling",
        "Running",
      ],
      datasets: [
        {
          label: "My First Dataset",
          fill: true,
          data: [65, 59, 90, 81, 56, 55, 40],
          backgroundColor: "rgba(255, 99, 132, 0.2)",
          borderColor: "rgb(255, 99, 132)",
          pointBackgroundColor: "rgb(255, 99, 132)",
          pointBorderColor: "#fff",
          pointHoverBackgroundColor: "#fff",
          pointHoverBorderColor: "rgb(255, 99, 132)",
          animation: {
            duration: 2000,
          },
        },
        {
          label: "My Second Dataset",
          data: [28, 48, 40, 19, 96, 27, 100],
          animation: {
            duration: 2000,
          },
          fill: true,
          backgroundColor: "rgba(54, 162, 235, 0.2)",
          borderColor: "rgb(54, 162, 235)",
          pointBackgroundColor: "rgb(54, 162, 235)",
          pointBorderColor: "#fff",
          pointHoverBackgroundColor: "#fff",
          pointHoverBorderColor: "rgb(54, 162, 235)",
        },
      ],
    },
  });
});
</script>
<style scoped>
.control__input {
  width: 100px;
}
</style>
