<script setup>
import { ref } from "vue";

const BOX_DATA = [
  [1, 1, 1],
  [1, 0, 0],
  [1, 1, 1],
];

const BOX_COUNT = BOX_DATA.flat().filter((box) => box !== 0).length;

const trackedSteps = ref([]);

const clickedPoint = (i, j) => `${i}${j}`;

let isDeSelecting = false;
const startDeSelection = async () => {
  isDeSelecting = true;
  for (let i = 0; i <= BOX_COUNT; i++) {
    await new Promise((resolve) => setTimeout(resolve, 1000));
    trackedSteps.value.shift();
  }
  isDeSelecting = false;
};

const onBoxClick = (clickedPoint) => {
  if (!trackedSteps.value.includes(clickedPoint)) {
    trackedSteps.value.push(clickedPoint);
  }
  if (BOX_COUNT === trackedSteps.value.length) {
    startDeSelection();
  }
};

const isClicked = (clickedPoint) => {
  return trackedSteps.value.includes(clickedPoint) ? "green-box" : "";
};
</script>

<template>
  <main class="main">
    <div>
      <div v-for="(row, i) in BOX_DATA" :key="i" class="row">
        <div v-for="(box, j) in row" :key="j" class="column">
          <button
            v-if="box !== 0"
            class="box-size box-design"
            :class="{
              'green-box': trackedSteps.includes(clickedPoint(i, j)),
            }"
            @click="onBoxClick(clickedPoint(i, j))"
          >
            <span
              v-if="!isDeSelecting && trackedSteps.includes(clickedPoint(i, j))"
            >
              {{ trackedSteps.indexOf(clickedPoint(i, j)) + 1 }}
            </span>
          </button>
          <div v-else class="box-size"></div>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
.main {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.row {
  display: flex;
  padding: 10px;
}

.column {
  display: flex;
  flex-direction: column;
  padding: 10px;
}

.box-size {
  height: 50px;
  width: 50px;
}

.box-design {
  height: 50px;
  width: 50px;
  border: 1px solid #000;
  cursor: pointer;
}

.green-box {
  background-color: #0bcc59;
}
</style>
