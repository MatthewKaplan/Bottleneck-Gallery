<template>
  <div class="img-container">
    <GalleryDescription
      class="description-area"
      v-bind:galleryInfo="this.galleryInfo"
      v-bind:galleryId="this.galleryId"
    />
    <br />
    <div class="btn-area" id="nav1" @click="$emit('return-btn')">
      <h2>
        Return To Galleries
        <img
          class="nav-icon"
          src="https://i.imgur.com/P7L54S6.png"
          alt="Return icon."
        />
      </h2>
    </div>
    <div class="img-container">
      <div v-bind:key="images.id" v-for="images in images">
        <Images
          v-on:return-btn="$emit('return-btn')"
          v-on:selected-image="$emit('selected-image', images)"
          v-bind:images="images"
        />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Images from "./Images";
import GalleryDescription from "./GalleryDescription";

export default {
  name: "ImageContainer",
  components: {
    Images,
    GalleryDescription
  },
  props: ["galleryId", "galleryInfo"],
  data() {
    return {
      images: []
    };
  },
  created() {
    axios
      .get(
        `https://api.harvardartmuseums.org/object?apikey=a6ce4310-b23f-11e9-8eb6-bf28e6d552d3&gallery=${this.galleryId}&size=100`
      )
      .then(
        results =>
          (this.images = results.data.records.filter(
            img => img.primaryimageurl
          ))
      )
      .catch(error => console.log(error));
  }
};
</script>

<style scoped>
.img-container {
  height: 88vh;
  width: 75.6vw;
  overflow: scroll;
  display: grid;
  grid-template-columns: 1fr 1fr;
  justify-items: center;
}

.image-container {
  display: grid;
  grid-template-columns: 1fr 1fr;
  margin-top: 75px;
  justify-items: center;
  grid-row-gap: 60px;
}

.description-area {
  background-color: #ddddcc;
  width: 350px;
  position: fixed;
  right: 0px;
  transition: 0.8s ease;
  box-shadow: 4px 5px 10px #000;
  top: 96px;
}

.btn-area {
  background-color: #ddddcc;
  width: 300px;
  height: 60px;
  border-radius: 30px;
  position: fixed;
  left: -238px;
  transition: 0.8s ease;
  box-shadow: 4px 5px 10px #000;
  cursor: pointer;
  z-index: 999;
}

.btn-area:hover {
  background-color: #262626;
  position: fixed;
  left: -50px;
  width: 300px;
  border: none;
  color: #fff;
  border-radius: 0;
}

.nav-icon {
  height: 50px;
  width: 50px;
  z-index: 999;
}

h2 img {
  position: absolute;
  left: 242px;
  bottom: 0px;
  color: #fff;
  font-size: 25px !important;
  padding-top: 4px;
  top: -21px;
}

h2 {
  font-family: baloo;
  font-weight: bold;
  position: relative;
  top: 20px;
  text-align: center;
  left: 0px;
  font-size: 20px;
  color: #fff;
}

#nav1 {
  top: 125px;
}
</style>
