<script setup>
import { ref } from 'vue';

let startTime = ref();
let endTime = ref();

let wage1 = ref();
let wage2 = ref();
let wage3 = ref();
let wage4 = ref();
let sum = ref(0);
let wageArray = ref([
    wage1, wage1, wage1, wage1, wage1, wage1,
  wage2, wage2, wage2, wage2, wage2, wage2,
  wage3, wage3, wage3, wage3, wage3, wage3,
  wage4, wage4, wage4, wage4, wage4, wage4
]);

const calculateWage = () => {
  if (startTime.value < endTime.value) {
    getNewArray();
    console.log("Start time is less than End time.")
  } else {
    getNewArray2();
    console.log("Start time is more than End time.")
  }
}
const getNewArray2 = () => {
  wageArray.value.splice(endTime.value, (startTime.value - endTime.value));
  sum = wageArray.value.reduce((a, b) => a + b.value, 0)
}
const getNewArray = () => {

    wageArray.value.splice(endTime.value)
    wageArray.value.splice(0, startTime.value)
    sum = wageArray.value.reduce((a, b) => a + b.value, 0)
}

const resetArray = () => {
  wageArray = ref([wage1, wage1, wage1, wage1, wage1, wage1,
    wage2, wage2, wage2, wage2, wage2, wage2,
    wage3, wage3, wage3, wage3, wage3, wage3,
    wage4, wage4, wage4, wage4, wage4, wage4]);
  wage1.value = 0;
  wage2.value = 0;
  wage3.value = 0;
  wage4.value = 0;
  startTime.value = ref();
  endTime.value = ref();
  sum = ref();
}

</script>

<template>
  <h1>Wage Calculator</h1>
  <form @submit.prevent="calculateWage">
    <div>
      <h3>Enter Shift Start and End Times</h3>
      <h5>Enter time in 24h format. Example: 5 (for 5am) and 17 (for 5pm). Midnight is 0.</h5>
      <h4>Shift Start:</h4><input type="number" v-model.number="startTime"/>
      <h4>Shift End:</h4><input type="number" v-model.number="endTime"/>
    </div>
    <div>
      <h3>Enter Wages For Each Time Block</h3>
      <h4>Midnight - 6AM:</h4><input type="number" v-model.number="wage1"/>
      <h4>6AM - Noon:</h4><input type="number" v-model.number="wage2"/>
      <h4>Noon - 6PM:</h4><input type="number" v-model.number="wage3"/>
      <h4>6PM - Midnight:</h4><input type="number" v-model.number="wage4"/>
    </div>
    <br/>
    <div>
      <button v-if="wageArray.length === 24" type="submit">Calculate Wages</button>
      <button v-if="wageArray.length !== 24" type="button" @click="resetArray">Reset</button>
      <h4>Total Earnings: ${{ sum }}</h4>
    </div>
  </form>
</template>
