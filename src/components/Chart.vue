<script>
import { Line } from "vue-chartjs";

export default {
  extends: Line,
  data() {
    return {
      options: {
        animation: {
          duration: 1500,
          easing: "linear",
        },
        scales: {
          yAxes: [
            {
              ticks: {
                suggestedMax: null,
              },
              scaleLabel: {
                display: true,
                labelString: "",
              },
            },
          ],
          xAxes: [
            {
              scaleLabel: {
                display: true,
                labelString: "",
              },
            },
          ],
        },
        responsive: true,
        maintainAspectRatio: false,
      },
    };
  },
  props: {
    labels: Array,
    futurevalue: Array,
    interest: Array,
    investment: Array,
  },
  computed: {
    chartData: function() {
      return this.futurevalue;
    },
  },
  watch: {
    futurevalue: function() {
      this.renderLineChart();
    },
  },
  methods: {
    renderLineChart() {
      this.renderChart(
        {
          labels: this.labels,
          datasets: [
            {
              lineTension: 0,
              label: "Future value",
              borderColor: "#85bb65", //dollar color #85bb65
              data: this.chartData,
              fill: false,
            },
            {
              lineTension: 0,
              label: "Total Interest",
              borderColor: "#ffa600",
              data: this.interest,
              fill: false,
            },
            {
              lineTension: 0,
              label: "Total Investment",
              borderColor: "#dd5182",
              data: this.investment,
              fill: false,
            },
          ],
        },
        this.options
      );
    },
  },
  mounted() {
    this.renderLineChart();
  },
};
</script>
