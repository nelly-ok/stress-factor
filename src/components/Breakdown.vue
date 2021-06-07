<template>
  <div class="breakdown-container">
    <div class="breakdown animate__animated animate__shakeY animate__repeat-3">
      <h3>uh oh, your stress level has gotten to high and you are having a nervous breakdown</h3>
      <h3>We'll explore coping methods later in the documentary, but for now lets ease up a little</h3>
      <button type="button" id="Right" class="btn btn-success" @click="destress">
          de-stress
      </button>
    </div>
  </div>
</template>


<script>


export default {
  
  name: "Breakdown",
  components: {
  },
  props: {
    msg: String,
  },
  methods: {
    start() {
      this.$emit("start");
    },
    prev() {
      this.$emit("prev");
    },
    next() {
      this.$emit("next");
    },
    destress() {
      console.log("destressing")
      this.$emit("destress")
    }
  },
};
</script>
ß
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>


.breakdown-container {
    background: #333a;
    z-index: 4;
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    display: flex;
    justify-content: center;
    align-items: center;
}

.breakdown {
  background-color: red;
  display: flex;
  padding: 2em;
    flex-direction: column;
    align-items: center;
    color: white;
}


</style>
