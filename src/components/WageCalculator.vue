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

const getNewArray = () => {
  wageArray.value.splice(endTime.value)
  wageArray.value.splice(0, startTime.value)
  sum = wageArray.value.reduce((a,b) => a + b.value)
}

</script>

<template>
  <h1>Wage Calculator</h1>
  <span>{{ wageArray }}</span>
  <form @submit.prevent="getNewArray">
    <div>
      <h3>Enter Shift Start and End Times</h3>
      <p>Enter time in 24h format</p>
      <p>Start:</p><input type="number" v-model.number="startTime"/>
      <p>{{ startTime }}</p>
      <p>End:</p><input type="number" v-model.number="endTime"/>
      <p>{{ endTime }}</p>
    </div>
    <div>
      <h3>Enter Wages For Each Time Block</h3>
      <p>Midnight - 6AM:</p><input type="number" v-model.number="wage1"/>
      <p>{{ wage1 }}</p>
      <p>6AM - Noon:</p><input type="number" v-model.number="wage2"/>
      <p>{{ wage2 }}</p>
      <p>Noon - 6PM:</p><input type="number" v-model.number="wage3"/>
      <p>{{ wage3 }}</p>
      <p>6PM - Midnight:</p><input type="number" v-model.number="wage4"/>
      <p>{{ wage4 }}</p>
    </div>
    <br/>
    <div>
      <button>Calculate Wages</button>
      <h4>Total Earnings: {{ sum }}</h4>
    </div>
  </form>
</template>
