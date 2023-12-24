<template>
  <section class="chart">
    <h1 class="chart__title" @click="test">Bubble Chart</h1>
    <p class="text-center">
      A <span class="chart-main-word">bubble chart</span> is used to display
      three dimensions of data at the same time. The location of the bubble is
      determined by the first two dimensions and the corresponding horizontal
      and vertical axes. The third dimension is represented by the size of the
      individual bubbles.
      <img
        src="../assets/Screenshot 2023-12-24 224340.png"
        alt=""
        class="ajab-sign"
      />
    </p>
    <div class="main-part">
      <div class="main-part__chart">
        <canvas ref="bubblechart_canvas"></canvas>
      </div>
      <div class="main-part__inputs">
        <transition-group class="each-controls" tag="div" name="list">
          <div class="controls" v-for="(item, i) in dummyArray" :key="i">
            <div class="control">
              <label for="x" class="control__label">X : </label>
              <input
                type="text"
                class="control__input"
                id="x"
                v-model="data[i].x"
              />
            </div>
            <div class="control">
              <label for="y" class="control__label">Y : </label>
              <input
                type="text"
                class="control__input"
                id="y"
                v-model="data[i].y"
              />
            </div>
            <div class="control">
              <label for="r" class="control__label">R : </label>
              <input
                type="text"
                class="control__input"
                id="r"
                v-model.number="data[i].r"
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
const bubblechart_canvas = ref();
const dummyArray = ref([1, 1, 1]);
const data = ref(
  Array.from(Array(100), () => {
    return {
      x: null,
      y: null,
      r: null,
    };
  })
);
function addControl() {
  dummyArray.value.push(1);
}

function createChart() {
  if (currentChart) currentChart.destroy();
  const fullArr = data.value.filter((item) => {
    if (!item.x || !item.y || !item.r) return false;
    else return true;
  });
  currentChart = new Chart(bubblechart_canvas.value, {
    type: "bubble",
    options: {},
    data: {
      datasets: [
        {
          backgroundColor: "rgb(255, 99, 132)",
          label: "My Chart",
          data: fullArr,
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
  currentChart = new Chart(bubblechart_canvas.value, {
    type: "bubble",
    options: {},
    data: {
      datasets: [
        {
          backgroundColor: "rgb(255, 99, 132)",
          label: "My Chart",
          data: [
            {
              x: 20,
              y: 30,
              r: 15,
            },
            {
              x: 40,
              y: 10,
              r: 10,
            },
          ],
          animation: {
            duration: 2000,
          },
        },
      ],
    },
  });
});
</script>
<style scoped>
.control__input {
  width: 50px;
}
</style>
