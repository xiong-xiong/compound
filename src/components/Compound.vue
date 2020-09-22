<template>
  <div class="compound">
    <h2>Calculate your compound interest</h2>
    <form class="vueContainer">
      <div class="formElement">
        <label for="principal">Your principal capital</label>
        <input v-model="principal" name="principal" type="number" />
      </div>
      <div class="formElement">
        <label for="addition">Your monthly addition</label>
        <input v-model="addition" name="addition" type="number" />
      </div>
      <div class="formElement">
        <label for="interest">Expected annual interest</label>
        <input v-model="interest" name="interest" type="number" />
      </div>
      <div class="formElement">
        <label for="years">Years to grow</label>
        <input v-model="years" name="years" type="number" />
      </div>
    </form>
    <button v-on:click="calculate">Calculate</button>
    <div class="output">{{ output }}$</div>

    <Chart :labels="labels" :datasets="dataPoints"> </Chart>
  </div>
</template>

<script>
import Chart from "./Chart.vue";

export default {
  name: "Compound",
  components: {
    Chart,
  },
  data() {
    return {
      principal: 10,
      addition: 1,
      interest: 5,
      years: 5,
      output: 0,
      labels: [], // for bar or line chart
      dataPoints: [], // for bar or line chart
    };
  },
  methods: {
    calculate() {
      let dataPoints = [];
      let labels = [];
      const interest = this.interest / 100;
      let futurevalue = this.principal;
      for (let index = 1; index <= this.years; index++) {
        const interestForValue =
          parseFloat(futurevalue) * (parseFloat(this.interest) / 100);
        const additionAnnual = parseFloat(this.addition) * 12;
        futurevalue =
          parseFloat(futurevalue) +
          parseFloat(interestForValue) +
          parseFloat(additionAnnual);
        // this calculates datapoints for chart
        const dataPoint = parseFloat(
          this.principal * Math.pow(1 + interest / 1, index).toFixed(2)
        );
        dataPoints.push(dataPoint);
        labels.push(index);
      }

      const answer = parseFloat(
        this.principal * Math.pow(1 + interest / 1, this.years)
      );
      this.dataPoints = dataPoints;
      this.labels = labels;
      this.output = futurevalue.toFixed(2);
      return answer;
    },
  },
  beforeMount() {
    this.calculate();
  },
};
</script>

<style scoped>
.formElement {
  display: grid;
  grid-template-columns: 1fr 1fr;
  text-align: left;
  margin-bottom: 20px;
}
.formElement label {
  display: block;
  width: auto;
}
.formElement input {
  display: block;
  width: 200px;
  height: 30px;
}
.vueContainer {
  width: 600px;
  max-width: 100%;
  margin: 0 auto;
}
</style>
