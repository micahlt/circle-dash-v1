<template>
<div>
  <h1>Circle Info</h1>
  <div class="restrictions">
    <table id="table" class="my-table">
      <tbody>
        <tr>
          <td class="first-col">{{data.circleEnabled}}</td>
          <td class="second-col">Enabled</td>
        </tr>
        <tr>
          <td class="first-col">{{data.circleID}}</td>
          <td class="second-col">MAC Address</td>
        </tr>
        <tr>
          <td class="first-col">{{data.circleTime}}</td>
          <td class="second-col">Time</td>
        </tr>
        <tr>
          <td class="first-col">{{data.circleDay}}</td>
          <td class="second-col">Day of Week</td>
        </tr>
        <tr>
          <td class="first-col">{{data.circleConnectedWifi}}</td>
          <td class="second-col">Network</td>
        </tr>
        <tr>
          <td class="first-col">{{data.weekend == "" ? 'False' : 'True'}}</td>
          <td class="second-col">Weekend</td>
        </tr>
      </tbody>
    </table>
  </div>
</div>
</template>

<script>
export default {
  name: 'CircleInfo',
  props: {
    data: Object
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

.restrictions {
  max-height: 40vh;
  overflow-y: auto;
  padding-bottom: 1em;
  margin-bottom: 1em;
}

li {
  display: inline;
  margin: 1em;
  color: rgb(98, 0, 238);
}

table {
  margin: auto;
}

.first-col {
  padding-right: 20px;
  text-align: right;
  color: rgb(98, 0, 238);
}

.second-col {
  color: #ccc;
  text-align: left;
}
</style>
