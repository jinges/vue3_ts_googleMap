<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <p>
      For a guide and recipes on how to configure / customize this project,<br>
      check out the
      <a href="https://cli.vuejs.org" target="_blank" rel="noopener">vue-cli documentation</a>.
    </p>
    <h3>Installed CLI Plugins</h3>
    <g-map
    :center='{ lat: 38.0, lng: -77.01 }'
    :start="start"
    :end="end"
    :waypoints="waypoints"
    :disableUI="false"
    :zoom="12"
    mapType="roadmap"
    >
</g-map>
  </div>
</template>

<script lang="ts">
import { ref } from 'vue';
import { Options, Vue } from 'vue-class-component';
import GMap from './GMap.vue';

@Options({
  props: {
    msg: String
  },
  components:{
    GMap
  }
})
export default class HelloWorld extends Vue {
  msg!: string;
  center: any = null;
  end  = {lat: 37.7577627, lng: -122.4726194};
  start = {lat: 42.3662514, lng: -71.0701804};
  waypoints: any = [{
      location: {lat: 39.7799642, lng: -86.2728331},
      stopover: true
    }, {
      location: {lat: 35.2020871, lng: -101.8749803},
      stopover: true
    }];

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
