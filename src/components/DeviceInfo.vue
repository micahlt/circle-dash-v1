<template>
<div>
  <h1>Device Info</h1>
  <div class="restrictions">
    <table id="table" class="my-table">
      <tbody>
        <tr>
          <td class="first-col">{{data.deviceName}}</td>
          <td class="second-col">Name</td>
        </tr>
        <tr>
          <td class="first-col">{{data.deviceID.toUpperCase()}}</td>
          <td class="second-col">MAC Address</td>
        </tr>
        <tr>
          <td class="first-col">{{data.deviceManufacturer}}</td>
          <td class="second-col">Manufacturer</td>
        </tr>
        <tr>
          <td class="first-col">{{data.role}}</td>
          <td class="second-col">Role</td>
        </tr>
        <tr>
          <td class="first-col">{{data.mode}}</td>
          <td class="second-col">Mode</td>
        </tr>
        <tr>
          <td class="first-col">{{data.deviceCount}}</td>
          <td class="second-col">Your Devices</td>
        </tr>
      </tbody>
    </table>
  </div>
</div>
</template>

<script>
export default {
  name: 'DeviceInfo',
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
