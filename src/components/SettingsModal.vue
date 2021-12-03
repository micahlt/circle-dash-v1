<template>
<div>
  <h1>User Restrictions</h1>
  <div class="restrictions">
    <ul>
      <li v-for="value in data" :key="value">{{value}}
      </li>
    </ul>
  </div>
</div>
</template>

<script>
export default {
  name: 'RestrictionsList',
  props: {
    data: Array
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
</style>
