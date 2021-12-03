<template>
<v-app>
  <v-app-bar density="compact">
    <v-app-bar-title>Circle Dash<span v-if="completed && !error"> for {{ res.info.username }}</span></v-app-bar-title>

    <v-spacer></v-spacer>
    <v-divider inset vertical></v-divider>
    <v-dialog v-model="dialog" persistent max-width="600px">
      <template v-slot:activator="{ props }">
        <v-btn v-bind="props" class="mr-4 ml-5" color="primary" plain>
          <v-icon left icon="mdi-cog-outline"></v-icon>

          <span>Settings</span>
        </v-btn>
      </template>
      <v-card>
        <v-card-title>
          <span class="text-h5">Settings</span>
        </v-card-title>
        <v-card-text>
          <v-container>
            <v-row>
              <v-col cols="12">
                <v-text-field label="Server IP" required v-model="serverIp"></v-text-field>
              </v-col>
            </v-row>
          </v-container>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="primary" plain text @click="dialog = false">
            Close
          </v-btn>
          <v-btn plain color="primary" text @click="updateServerIp">
            Save
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-app-bar>

  <v-main>
    <v-progress-linear indeterminate color="deep-purple" v-if="!completed"></v-progress-linear>
    <v-container class="grey lighten-5" v-if="completed && !error">
      <v-row>
        <v-col>
          <v-card elevation="2" class="fill-height">
            <PieChart :data="res.info.categoryusage" />
          </v-card>
          <v-card elevation="2" class="fill-height">
            <CircleInfo :data="res.info"></CircleInfo>
          </v-card>
        </v-col>
        <v-col>
          <v-card elevation="2" class="fill-height">
            <CategoryUsage :data="res.info.categoryusage"></CategoryUsage>
          </v-card>
          <v-card elevation="2" class="fill-height">
            <RestrictionsList :data="res.info.enabled"></RestrictionsList>
          </v-card>
          <v-card elevation="2" class="fill-height">
            <FilteredList :data="res.info.filtered"></FilteredList>
          </v-card>
        </v-col>
        <v-col>
          <v-card elevation="2" class="fill-height">
            <SiteUsage :data="res.info.siteusage.all"></SiteUsage>
          </v-card>
          <v-card elevation="2" class="fill-height">
            <DeviceInfo :data="res.info"></DeviceInfo>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
    <v-container class="error-container" v-if="completed && error">
      <v-row>
        <v-col align-self="center" class="error">
          <h2>Error</h2>
          <p>Please ensure that you have the correct server IP set in settings.</p>
        </v-col>
      </v-row>
    </v-container>
  </v-main>
</v-app>
</template>

<script>
import PieChart from './components/PieChart.vue'
import CategoryUsage from './components/CategoryUsage.vue'
import SiteUsage from './components/SiteUsage.vue'
import DeviceInfo from './components/DeviceInfo.vue'
import CircleInfo from './components/CircleInfo.vue'
import RestrictionsList from './components/RestrictionsList.vue'
import FilteredList from './components/FilteredList.vue'

export default {
  name: 'App',
  components: {
    PieChart,
    CategoryUsage,
    RestrictionsList,
    SiteUsage,
    DeviceInfo,
    CircleInfo,
    FilteredList
  },
  data() {
    if (!window.localStorage.getItem('serverIp')) {
      window.localStorage.setItem('serverIp', '192.168.1.1:4444');
    }
    return {
      completed: false,
      res: {},
      dialog: false,
      serverIp: window.localStorage.getItem('serverIp'),
      error: false
    }
  },
  mounted() {
    this.refreshData();
  },
  methods: {
    updateServerIp() {
      this.dialog = false;
      window.localStorage.setItem('serverIp', this.serverIp);
      this.refreshData();
    },
    refreshData() {
      let that = this;
      that.error = false;
      that.completed = false;
      fetch(`http://${that.serverIp}/api/USERINFO`)
        .then((res) => {
          return res.json();
        })
        .then((data) => {
          that.res = data;
          that.completed = true;
        }).catch((error) => {
          console.log(error);
          that.error = true;
          that.completed = true;
        })
    }
  }
}
</script>
<style>
.fill-height {
  height: 100%;
}

*::-webkit-scrollbar {
  width: 10px;
}

*::-webkit-scrollbar-track {
  background: transparent;
}

*::-webkit-scrollbar-thumb {
  background: rgba(0, 0, 0, 0.2);
  border: solid 3px white;
  border-radius: 8px;
}

*::-webkit-scrollbar-thumb:hover {
  background: rgb(106, 0, 211, 0.5);
}

.v-card {
  height: min-content;
  margin-bottom: 1.5em;
}

.error h2 {
  text-align: center;
  color: rgb(98, 0, 238);
}

.error p {
  text-align: center;
  color: black;
}

.error-container,
.error-container .v-row {
  height: 100%;
}
</style>
