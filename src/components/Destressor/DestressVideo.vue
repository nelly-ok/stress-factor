<template>
  <div class="home">
    <h1>{{header}}</h1>
    <iframe
      width="560"
      height="315"
      :src="source"
      title="YouTube video player"
      frameborder="0"
      allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
      allowfullscreen
    ></iframe>
    <button type="button" id="Right" class="btn btn-success" style="margin-top: 0.75em" @click="back" >
         Back &lt; &lt;
      </button>
  </div>
</template>

<script>


export default {
  
  name: "Video",
  components: {
  },
  props: {
    source: String,
    header: String
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
    back(){
      this.$emit("back");
    },
  },
};
</script>
ß
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.home {
  width: 100%;
  height: 100%;
}

iframe {
      width: 100%;
    height: 100%;
}
</style>
