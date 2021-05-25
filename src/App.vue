<template>
  <div id="app">
    <button @click="randomNumber">BMI</button>

    <h2>{{ randomNum }}</h2>
    <div v-if="this.randomNum > 0">
      <h4>Your BMI is {{ bmi }}</h4>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      randomNum: "",
      bmi: "",
    };
  },
  methods: {
    randomNumber() {
      this.randomNum = Math.floor(Math.random() * 20) + 15;
      if (parseInt(this.randomNum) < 18.9) {
        this.bmi = "Underweight";
      } else if (
        parseInt(this.randomNum) >= 18.9 &&
        parseInt(this.randomNum) < 25
      ) {
        this.bmi = "Normal weight";
      } else if (
        parseInt(this.randomNum) >= 25 &&
        parseInt(this.randomNum) < 30
      ) {
        this.bmi = "Overweight";
      } else if (parseInt(this.randomNum) >= 30) {
        this.bmi = "Obesity";
      }
    },
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
