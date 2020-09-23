<template>
  <div class="compound">
    <h2>Calculate compound interest</h2>
    <form class="vueContainer">
      <div class="formElement">
        <label for="principal">Principal capital</label>
        <input
          v-model="principal"
          name="principal"
          type="number"
          @change="calculate"
        />
      </div>
      <div class="formElement">
        <label for="addition">Monthly addition</label>
        <input
          v-model="addition"
          name="addition"
          type="number"
          @change="calculate"
        />
      </div>
      <div class="formElement">
        <label for="interest">Expected annual interest</label>
        <input
          v-model="interest"
          name="interest"
          type="number"
          @change="calculate"
        />
      </div>
      <div class="formElement">
        <label for="years">Years to grow</label>
        <input v-model="years" name="years" type="number" @change="calculate" />
      </div>
    </form>
    <div class="vueContainer">
      <button class="calcBtn" v-on:click="calculate">
        Calculate
      </button>
      <div class="outputContainer">
        <div class="output">Total interest: {{ totalInterest }} $</div>
        <div class="output">Total investment: {{ totalInvestedAmount }} $</div>
        <div class="output">Future value: {{ futurevalue }} $</div>
      </div>
    </div>
    <Chart
      :labels="labels"
      :futurevalue="dataPoints"
      :interest="interestDataPoints"
      :investment="investmentDataPoints"
    >
    </Chart>
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
      principal: 5000,
      addition: 100,
      interest: 5,
      years: 5,
      futurevalue: 0,
      totalInterest: 0,
      totalInvestedAmount: 0,
      labels: [], // for bar or line chart
      dataPoints: [], // for bar or line chart
      interestDataPoints: [], // for bar or line chart
      investmentDataPoints: [], // for bar or line chart
    };
  },
  methods: {
    calculate() {
      let dataPoints = [];
      let interestDataPoints = [];
      let investmentDataPoints = [];
      let labels = [];
      //const interest = this.interest / 100;
      let futurevalue = this.principal;
      let interestTotal = 0;
      for (let index = 1; index <= this.years; index++) {
        const interestForValue =
          parseFloat(futurevalue) * (parseFloat(this.interest) / 100);
        const additionAnnual = parseFloat(this.addition) * 12;

        // FUTURE VALUE NUM
        futurevalue =
          parseFloat(futurevalue) +
          parseFloat(interestForValue) +
          parseFloat(additionAnnual);
        // INTEREST TOTAL NUM
        interestTotal = interestTotal + interestForValue;

        // CHART DATAPOINTS
        interestDataPoints.push(interestTotal.toFixed(0));
        investmentDataPoints.push((futurevalue - interestTotal).toFixed(0));
        dataPoints.push(futurevalue.toFixed(0));
        labels.push("Year " + index);
      }

      this.dataPoints = dataPoints;
      this.interestDataPoints = interestDataPoints;
      this.investmentDataPoints = investmentDataPoints;
      this.labels = labels;
      this.futurevalue = futurevalue.toFixed(0);
      this.totalInterest = interestTotal.toFixed(0);
      this.totalInvestedAmount = (futurevalue - interestTotal).toFixed(0);
    },
  },
  beforeMount() {
    this.calculate();
  },
};
</script>

<style scoped>
h2 {
  border-bottom: 4px solid #333;
}
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
.calcBtn {
  outline: none;
  background: #333;
  color: white;
  height: 50px;
  width: 100%;
  line-height: 50px;
  padding: 0;
  border: 0;
  cursor: pointer;
  margin-bottom: 25px;
}
.calcBtn:hover {
  opacity: 0.9;
}
.outputContainer {
  font-size: 1.4rem;
  text-align: left;
  margin-bottom: 25px;
  border: 2px solid #333;
  padding: 5px;
}
</style>
