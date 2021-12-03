<template>
<div>
  <h1>Total Visits</h1>
  <canvas id="myChart" width="300" height="300"></canvas>
  <h2>{{total}}</h2>
  <p>web requests</p>
</div>
</template>

<script>
import Chart from 'chart.js/auto';
export default {
  name: 'PieChart',
  props: {
    data: Object
  },
  data() {
    return {
      total: 0
    }
  },
  mounted() {
    var parsedData = this.data;
    var keys = Object.keys(parsedData);
    keys.shift();
    var values = [];
    keys.forEach((item, i) => {
      console.log(item);
      if (i > 0) {
        values.push(parsedData[Object.keys(parsedData)[i]]);
        this.total += parseInt(parsedData[Object.keys(parsedData)[i]]);
      }
    })
    const ctx = document.getElementById('myChart').getContext('2d');
    new Chart(ctx, {
      type: 'pie',
      data: {
        labels: keys,
        datasets: [{
          label: 'Dataset 1',
          data: values,
          backgroundColor: ['#7200ED']
        }]
      },
      options: {
        responsive: true,
        plugins: {
          legend: {
            position: 'top',
            display: false
          },
          title: {
            display: false,
            text: 'Chart.js Pie Chart'
          }
        }
      },
    });
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
div {
  display: block;
  text-align: center;
}

h1 {
  text-align: center;
  padding: 15px;
  font-size: 1.2em;
  font-weight: normal;
}

canvas {
  margin: auto;
  padding: 20px;
}

h2 {
  font-size: 2em;
  line-height: 1em;
}

p {
  margin-bottom: 1em;
  font-size: 0.8em;
}
</style>
