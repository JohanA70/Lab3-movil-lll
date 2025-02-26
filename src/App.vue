<script setup>
import { ref, computed } from 'vue';

const temperature = ref('');
const fromUnit = ref('');
const toUnit = ref('');
const result = ref('');

const convert = () => {
  let temp = parseFloat(temperature.value);
  if (isNaN(temp)) return;
  let converted;

  if (fromUnit.value === toUnit.value) {
    converted = temp;
  } else if (fromUnit.value === 'Celsius' && toUnit.value === 'Fahrenheit') {
    converted = (temp * 9 / 5) + 32;
  } else if (fromUnit.value === 'Celsius' && toUnit.value === 'Kelvin') {
    converted = temp + 273.15;
  } else if (fromUnit.value === 'Fahrenheit' && toUnit.value === 'Celsius') {
    converted = (temp - 32) * 5 / 9;
  } else if (fromUnit.value === 'Fahrenheit' && toUnit.value === 'Kelvin') {
    converted = (temp - 32) * 5 / 9 + 273.15;
  } else if (fromUnit.value === 'Kelvin' && toUnit.value === 'Celsius') {
    converted = temp - 273.15;
  } else if (fromUnit.value === 'Kelvin' && toUnit.value === 'Fahrenheit') {
    converted = (temp - 273.15) * 9 / 5 + 32;
  }

  result.value = `${temperature.value} ${fromUnit.value} is ${converted.toFixed(2)} ${toUnit.value}`;
};
</script>

<template>
  <div id="app">
    <div class="container">
      <h2 class="mF2">Temperature Converter</h2>
      <p class="mF">Enter the temperature, select units and submit</p>
      <div class="funtions">
        <input type="number" v-model="temperature" placeholder="0.00">
        <select v-model="fromUnit">
          <option value="">From Unit</option>
          <option value="Celsius">Celsius</option>
          <option value="Fahrenheit">Fahrenheit</option>
          <option value="Kelvin">Kelvin</option>
        </select>
        <select v-model="toUnit">
          <option value="">To Unit</option>
          <option value="Celsius">Celsius</option>
          <option value="Fahrenheit">Fahrenheit</option>
          <option value="Kelvin">Kelvin</option>
        </select>
        <button @click="convert" :disabled="!temperature || !fromUnit || !toUnit">Convert</button>

      </div>
      <p v-if="result" class="result">{{ result }}</p>
    </div>
  </div>
</template>

<style scoped>
body {
  font-family: Arial, sans-serif;
  height: 100vh;
  background-color: #f8f8f8;
}

.container {
  background: white;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  width: 660px;
}

.funtions {
  display: flex;
}

.mF {
  color: black;
  margin-bottom: 30px;
}

.mF2 {
  color: black;
  margin-bottom: 5px;
}

input,
select,
button {
  padding: 10px;
  font-size: 16px;
  border-radius: 5px;
  border: 1px solid #ccc;
}

button {
  background-color: black;
  color: white;
  cursor: pointer;
}

button:disabled {
  background-color: gray;
  cursor: not-allowed;
}

.result {
  margin-top: 15px;
  font-size: 18px;
  color: green;
}
</style>