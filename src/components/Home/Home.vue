<template>
  <section>
    <Home1 v-if="home[0]" @prev="prev(0)" @next="next(0)"/>
    <Home2 v-if="home[1]" @prev="prev(1)" @next="next(1)"/>
    <Home3Start v-if="home[2]" @start="start" @prev="prev(2)"/>

  </section>
</template>

<script>

import Home1 from './Home1'
import Home2 from './Home2'
import Home3Start from './Home3Start'


export default {
  name: "Home",
  props: {
    msg: String,
  },
  components: {
    Home1,
    Home2,
    Home3Start
  },
  data(){
    return {
      home: {0: true, 1: false, 2:false}
    }
  },
  methods: {
    start(value) {
      console.log(value);
      this.$emit("start", value);
    },
    prev(val) {
      if (val != 0) {
        this.home[val] = false;
        this.home[val - 1] = true;
      }
      if (val == 2){
        this.$emit("unstarted");
      }
      
    },
    next(val) {
      if (val < 3){
        this.home[val] = false;
        this.home[val + 1] = true;
      }
      if (val == 1){
        this.$emit("started");
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.identity-select {
  display: flex;
  width: 100%;
  padding: 0 3em;
  justify-content: space-between;
}

.home {
  display: flex;
  padding: 4em;
  flex-direction: column;
  align-items: center;
  justify-content: space-around;
}

.select-third {
  width: 25%;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.stat-img {
  width: 65%;
}
</style>
