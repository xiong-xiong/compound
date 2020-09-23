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
    datasets: Array,
  },
  computed: {
    chartData: function() {
      return this.datasets;
    },
  },
  watch: {
    datasets: function() {
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
              label: "Value",
              borderColor: "green",
              data: this.chartData,
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
