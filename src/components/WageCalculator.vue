<script setup>
import {ref} from 'vue';

let startTime = ref();
let endTime = ref();
let msg = ref("Calculate Wages")
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
  if (wageArray.value.length === 24) {
    if (startTime.value < endTime.value) {
      getNewArray();
      msg.value = "Reset";
    } else {
      getNewArray2();
      msg.value = "Reset";
    }
  } else {
    resetArray();
    msg.value = "Calculate Wages";
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
  wage1.value = ref();
  wage2.value = ref();
  wage3.value = ref();
  wage4.value = ref();
  startTime.value = ref();
  endTime.value = ref();
  sum = ref();
}
</script>

<template>
  <div class="hero min-h-screen bg-base-200">
    <div class="hero-content text-center">
      <div class="max-w-md">
        <h1 class="text-3xl text-blue-700 pb-4">Wage Calculator</h1>
        <form @submit.prevent="calculateWage">
          <div class="pb-4">
            <h3 class="text-lg font-bold">Enter Shift Start and End Times</h3>
            <h5 class="text-sm pb-4">Enter time in 24h format. Example: 5 (for 5am) and 17 (for 5pm). Midnight is 0.</h5>
            <h4 class="font-bold">Shift Start:</h4><input type="number" v-model.number="startTime" class="input input-bordered w-full max-w-xs"/>
            <h4 class="font-bold">Shift End:</h4><input type="number" v-model.number="endTime" class="input input-bordered w-full max-w-xs"/>
          </div>
          <div>
            <h3 class="text-lg font-bold pb-4">Enter Wages For Each Time Block</h3>
            <h4 class="font-bold">Midnight - 6AM:</h4><input type="number" v-model.number="wage1" class="input input-bordered w-full max-w-xs"/>
            <h4 class="font-bold">6AM - Noon:</h4><input type="number" v-model.number="wage2" class="input input-bordered w-full max-w-xs"/>
            <h4 class="font-bold">Noon - 6PM:</h4><input type="number" v-model.number="wage3" class="input input-bordered w-full max-w-xs"/>
            <h4 class="font-bold">6PM - Midnight:</h4><input type="number" v-model.number="wage4" class="input input-bordered w-full max-w-xs"/>
          </div>
          <br/>
          <div>
            <button type="submit" class="btn btn-wide">{{ msg }}</button>
            <h4 class="font-bold text-xl text-green-500 pt-4">Total Earnings: ${{ sum }}</h4>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>
