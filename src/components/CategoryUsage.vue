<template>
<div>
  <h1>Usage per Category</h1>
  <div class="categories">
    <table id="table" class="my-table">
      <thead>
        <tr>
          <td>Visits</td>
          <td>Category</td>
        </tr>
      </thead>
      <tbody>
        <tr v-for="value in values" :key="value">
          <td class="first-col">{{value.num}}</td>
          <td class="second-col">{{value.name}}</td>
        </tr>
      </tbody>
    </table>
  </div>
</div>
</template>

<script>
export default {
  name: 'CategoryUsage',
  props: {
    data: Object
  },
  data() {
    var parsedData = this.data;
    var keys = Object.keys(parsedData);
    keys.shift();
    var values = [];
    keys.forEach((item, i) => {
      console.log(item);
      values.push({
        num: parsedData[Object.keys(parsedData)[i + 1]],
        name: item
      });
    });
    return {
      values
    };
  },
  mounted() {
    function sortTable() {
      var table, rows, switching, i, x, y, shouldSwitch;
      table = document.querySelector('.my-table');
      switching = true;
      while (switching) {
        // Start by saying: no switching is done:
        switching = false;
        rows = table.rows;
        for (i = 1; i < (rows.length - 1); i++) {
          // Start by saying there should be no switching:
          shouldSwitch = false;
          x = rows[i].getElementsByTagName("td")[0];
          y = rows[i + 1].getElementsByTagName("td")[0];
          // Check if the two rows should switch place:
          if (Number(x.innerHTML) < Number(y.innerHTML)) {
            // If so, mark as a switch and break the loop:
            shouldSwitch = true;
            break;
          }
        }
        if (shouldSwitch) {
          rows[i].parentNode.insertBefore(rows[i + 1], rows[i]);
          switching = true;
        }
      }
    }
    sortTable();
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
div {
  display: block;
}

h1 {
  text-align: center;
  padding: 15px;
  font-size: 1.2em;
  font-weight: normal;
}

.categories {
  max-height: 40vh;
  overflow-y: auto;
  padding-bottom: 1em;
  margin-bottom: 1em;
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
}
</style>
