<template>
    <section>
      <Home v-if="home" @start="start" msg="Welcome to Your Vue.js App"/>
      <Stress v-if="stress" />
    </section>
</template>

<script>
import Home from './components/Home.vue'
import Stress from './components/Stress.vue'

export default {
  name: 'App',
  components: {
    Home,
    Stress
  },
  data() {
    return {
      home: true,
      stress: false
    }
  },
  methods: {
    start(){
      console.log("start")
      this.home = false;
      this.stress = true;
    }
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
