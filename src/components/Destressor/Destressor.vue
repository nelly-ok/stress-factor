
<template>
  <section class="destressor" > 
    <div class="destressor actual" v-if="!selected" > 
      <h1>De-stressors</h1>
      <div class="grid">
        <div class="grid-item" v-for="item in stressGrid" :key="item" @click="select(item)">
          <img :src="getImg(item.img)" alt="" srcset="">
          <h3>{{item.header}}</h3>
        </div>
      </div>
       <button type="button" id="Right" class="btn btn-success" style="margin-top: 0.75em" @click="done" >
        Done De-stressing - Back to the documentary
      </button>
    </div>

    <destress-video v-if="selected" :header="selected.header" :source="selected.source" @back="back"/>
  </section>
</template>


<script>
import DestressVideo from './DestressVideo.vue';

export default {
  
  name: "Breakdown",
  components: {
    DestressVideo
  },
  props: {
    msg: String,
  },
  data() {
    return {
      selected: false,
      stressGrid: [{
          header: "Nature Walk",
            img: "walk", 
            source: "https://www.youtube.com/embed/q1m27R0tAKM"
          }, {
            header: "Nature Ambience",
            img: "ambience",
            source: "https://www.youtube.com/embed/4zqKJBxRyuo"
          }, {
            header: "Mindful breathing",
            img: "breathing",
            source: "https://www.youtube.com/embed/nmFUDkj1Aq0"
          }, {
            header: "Alan Watts",
            img: "watts",
            source: "https://www.youtube.com/embed/jPpUNAFHgxM"
          }, {
            header: "Guided Meditation",
            img: "meditation",
            source: "https://www.youtube.com/embed/nIb2LbqHtY4"
          }, {
            header: "Yoga",
            img: "yoga",
            source: "https://www.youtube.com/embed/sTANio_2E0Q"
          }, {
            header: "Lo-fi Relaxing Music",
            img: "lofi",
            source: "https://www.youtube.com/embed/5qap5aO4i9A"
          }, {
            header: "Cute Cats",
            img: "cats",
            source: "https://www.youtube.com/embed/uHKfrz65KSU"
          }, {
            header: "Cute Dogs",
            img: "dogs",
            source: "https://www.youtube.com/embed/X2lIovmNsUY"
          }
          ]
    }
  },
  methods: {
    getImg(name){
      var images = require.context('../../assets/img/', false, /\.jpg$/)
      return images('./' + name + ".jpg")
    },
    select(item) {
      this.selected=item
    },
    back(){
      this.selected = false;
    },
    done(){
      this.$emit("finishDestress");
    }
  },
};
</script>
ß
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.actual {
  padding: 5em;
}

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
    flex-direction: column
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
  margin-top: 1em;
  display: flex;
    flex-direction: column;
    align-items: center;
}

.grid-item img {
  width: 50%;
}

.grid-item h3 {
  margin-top: 0.5em;
}




</style>
