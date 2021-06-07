
<template>
  <div class="destressor">
    <div class="grid">
      <div class="grid-item" v-for="item in stressGrid" :key="item">
        <img :src="getImg('income')" alt="" srcset="">
        <h3>Shits</h3>
      </div>
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
  data() {
    return {
      stressGrid: [0, 1, 2, 3, 4, 5, 6, 7, 8]
    }
  },
  methods: {
    getImg(name){
      var images = require.context('../../assets/img/', false, /\.jpg$/)
      return images('./' + name + ".jpg")
    },
  },
};
</script>
ß
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>


.destressor {
  z-index: 10;
  background-color: dodgerblue;
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    display: flex;
    justify-content: center;
    align-items: center;
}

.grid {
  width: 100%;
  height: 100%;
  display: flex;
  flex-flow: row wrap;
}

.grid-item {
  width: 33%;
  height: 33%;
  display: flex;
    flex-direction: column;
    align-items: center;
}

.grid-item img {
  width: 50%;
}

.grid-item h3 {
  margin-top: 0.75em;
}




</style>
