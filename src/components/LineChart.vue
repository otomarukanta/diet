<script lang="ts">
import { Component, Mixins, Prop } from 'vue-property-decorator';
import Chart from 'chart.js';

import { Line } from 'vue-chartjs';

@Component({})
export default class LineChart extends Mixins(Line) {
  @Prop() public weights!: any[];
  @Prop() public chartData!: Chart.ChartData;
  @Prop() public chartOptions: Chart.ChartOptions = {
    responsive: true,
    maintainAspectRatio: false,
    legend: {
      display: false,
      onClick(event, legendItem) {
        return;
      },
    },
    scales: {
      xAxes: [
        {
          type: 'time',
          distribution: 'linear',
          bounds: 'ticks',
          ticks: {
            source: 'labels'
          },
          time: {
            unit: 'month',
            displayFormats: {
              day: 'YYYY/MM/DD',
              month: 'YYYY/MM'
            }
          }
        },
      ],
      yAxes: [
        {
          id: 'yAxis_1',
          type: 'linear',
          scaleLabel: {
            display: true,
            labelString: '体重(kg)',
          },
          ticks: {
            min: 70,
            max: 100,
          },
        },
      ],
    },
  };

  public created() {
    this.createChartData();
  }

  public mounted() {
    this.renderChart(this.chartData, this.chartOptions);
  }

  public createChartData() {
    this.chartData = {
      labels: ['2019-04-01', '2020-04-01'],
      datasets: [
        {
          yAxisID: 'yAxis_1',
          type: 'line',
          label: '計測値',
          borderColor: '#6090EF',
          fill: false,
          data: this.weights,
        },
        {
          yAxisID: 'yAxis_1',
          type: 'line',
          label: '目標値',
          borderColor: '#0090EF',
          fill: false,
          data: [
            {t: new Date('2019-09-01'), y: 90.7},
            {t: new Date('2019-10-01'), y: 89.6},
            {t: new Date('2019-11-01'), y: 88.5},
            {t: new Date('2019-12-01'), y: 87.4},
            {t: new Date('2020-01-01'), y: 86.3},
            {t: new Date('2020-02-01'), y: 85.2},
            {t: new Date('2020-03-01'), y: 84.1},
            {t: new Date('2020-04-01'), y: 83.0},
            {t: new Date('2020-05-01'), y: 81.9},
            {t: new Date('2020-06-01'), y: 80.8},
            {t: new Date('2020-07-01'), y: 79.7},
            {t: new Date('2020-08-01'), y: 78.6},
            {t: new Date('2020-09-01'), y: 77.5},
            {t: new Date('2020-10-01'), y: 76.4},
            {t: new Date('2020-11-01'), y: 75.3},
            {t: new Date('2020-12-01'), y: 74.2},
            {t: new Date('2021-01-01'), y: 73.1},
            {t: new Date('2021-02-01'), y: 72},
          ],
        },
      ],
    };
  }
}
</script>