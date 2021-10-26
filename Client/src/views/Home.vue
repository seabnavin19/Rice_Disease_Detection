<template>
  <div id="app">
      <DropImage />
  
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from "@/components/HelloWorld.vue";
import DropImage from "../components/DropImage.vue"
// import Slides from "../components/slides.vue"

export default {
  name: "Home",
  components: {
  
    DropImage,
    // Slides
  },
};
</script>
