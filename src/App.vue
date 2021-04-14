<template>
  <div id="app">
    <h1>Profile demo</h1>
    <profile-demo/>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import ProfileDemo from './components/ProfileDemo.vue';

@Component({
  components: {
    ProfileDemo,
  },
})
export default class App extends Vue {}
</script>

<style>
body {
  font-size: 16pt;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
