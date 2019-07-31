<template>
  <div class="accordion">
    <ul>
      <GallerySlides v-bind:galleryInfo="galleryInfo"/>
    </ul>
  </div>
</template>

<script>
import axios from "axios";
import GallerySlides from "./GallerySlides";

export default {
  name: "Gallery",
  data() {
    return {
      galleryInfo: []
    };
  },
  components: {
    GallerySlides
  },
  created() {
    axios
      .get(
        `https://api.harvardartmuseums.org/gallery?apikey=a6ce4310-b23f-11e9-8eb6-bf28e6d552d3&size=64`
      )
      .then(
        results =>
          (this.galleryInfo = results.data.records.filter(
            gallery => gallery.objectcount > 25 && gallery.theme !== null
          ))
      )
      .catch(error => console.log(error));
  }
};
</script>

<style>
.accordion {
  width: 100vw;
  height: 87vh;
  overflow: hidden;
  box-shadow: 0 10px 6px -6px #111;
  margin: 0px auto;
}
.accordion ul {
  width: 200%;
}

.accordion li {
  position: relative;
  display: block;
  width: 60px;
  float: left;
  box-shadow: 0 0 30px 8px #222;
  transition: all 0.8s ease 0.5ms;
}

.accordion ul:hover li {
  width: 40px;
}
.accordion ul li:hover {
  width: 640px;
}

.caption {
  background: rgba(0, 0, 0, 0.7);
  position: absolute;
  bottom: 0;
  width: 640px;
  left: 5vw;
  transition: all 0.5s ease 0.5ms;
  text-align: center;
}

.caption a {
  display: block;
  color: #fff;
  text-decoration: none;
  font: normal 16px "Lato", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  padding: 15px;
}
</style>
