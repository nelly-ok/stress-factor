<template>
  <div class="home">
    <h1>Spin the life expectancy wheel</h1>
    <div class="wheel-container">
      <img class="wheel bg" src="../assets/img/wheel-bg.png" alt="" srcset="" />
      <img
        class="wheel fg"
        id="FG"
        src="../assets/img/wheel-fg.png"
        alt=""
        srcset=""
      />
    </div>
    <NextButton @prev="prev" @next="next" />
    <div class="results">
      <button type="button" class="btn btn-success" @click="spin">Spin</button>
      <p>Result: {{result}}</p>
    </div>
  </div>
</template>

<script>
import NextButton from "./NextButton.vue";

export default {
  name: "LifeWheel",
  components: {
    NextButton,
  },
  props: {
    msg: String,
  },
  data() {
    return {
      result: ""
    }
  },
  methods: {
    spin() {
      var deg = 0;
      const interval = setInterval(function () {
        deg +=20;
        var wheel = document.getElementById("FG");
        wheel.style.webkitTransform = "rotate(" + deg + "deg)";
        wheel.style.mozTransform = "rotate(" + deg + "deg)";
        wheel.style.msTransform = "rotate(" + deg + "deg)";
        wheel.style.oTransform = "rotate(" + deg + "deg)";
        wheel.style.transform = "rotate(" + deg + "deg)";
      }, 100);

      //Stop the functions after 1 minute.
      setTimeout(function () {
        clearInterval(interval);
      }, 3000);
    },
    prev() {
      this.$emit("prev");
    },
    next() {
      this.$emit("next");
    },
  },
};
</script>
ß
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.wheel {
  width: 300px;
  position: absolute;
  
}

.wheel-container {
  position: relative;
    top: -150px;
    left: -150px;
}
.results {
  position: relative;
    bottom: -5em;
}

.bg {
  z-index: 3;
}

.home h1 {
  position: relative;
  top: -3em;
}
</style>
