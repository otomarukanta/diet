<template>
  <div id="app">
    a
    <LineChart v-if="loaded" :weights="weights"/>
    b
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import LineChart from '@/components/LineChart.vue';
import axios from 'axios';

@Component({
  components: {
    LineChart,
  },
})
export default class App extends Vue {
  private weights: any[] = [];
  private loaded: boolean = false;

  private mounted() {
    axios.get('https://thingspeak.com/channels/560810/field/1.json?start=2019-01-01%2000:00:00').then(
      res => {
        var feeds: any[] = res.data.feeds;
        this.weights = feeds.map(x => {return {t: new Date(x.created_at), y: Number(x.field1)}});
        this.loaded = true;
        console.log(this.weights);
      },
    );
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
