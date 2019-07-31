<template>
<div>
  <h1>Choose a gallery you would like to view:</h1>
</div>
  
</template>

<script>
import axios from "axios";

export default {
  name: "Gallery",
  data() {
    return {
      galleries: []
    }
  },
  created() {
    axios.get(
      `https://api.harvardartmuseums.org/gallery?apikey=a6ce4310-b23f-11e9-8eb6-bf28e6d552d3&size=64`
    )
      .then(results => (this.galleries = results.data.records.filter(gallery => gallery.objectcount > 25 && gallery.theme !== null)))
      .catch(error => console.log(error));
  }
}
</script>

<style>

</style>
