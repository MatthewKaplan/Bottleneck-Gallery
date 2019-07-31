<template>
  <div class="gallery-slides">
    <div v-bind:key="gallery.id" v-for="gallery in galleries.galleryArray" @mouseover="isHovering = true" @mouseout="isHovering = false">
      <li>
        <div v-bind:class="{'not-caption':(isHovering === false), 'caption':(isHovering === true)}">
          <a href="#">{{gallery.name}}</a>
          <a class="gallery-theme" href="#">{{gallery.theme}}</a>
        </div>
        <a href="#">
          <img v-bind:src="gallery.image" />
        </a>
      </li>
    </div>
  </div>
</template>

<script>
import galleryArray from "../../helper/data";

export default {
  name: "GallerySlides",
  props: ["galleryInfo"],
  data() {
    return {
      galleries: [],
      isHovering: false
    };
  },
  created() {
    this.galleries = galleryArray;
  }
};
</script>

<style>
img {
  height: 87vh;
  width: 800px;
}
.gallery-slides {
  height: 100%;
}

.not-caption {
  background: rgba(0, 0, 0, 0.7);
  position: absolute;
  bottom: 0px;
  left: 100vw;
  width: 640px;
  transition: all 0.5s ease 0.5ms;
}

.not-caption a {
  display: block;
  color: #fff;
  text-decoration: none;
  font: normal 16px "Lato", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  padding: 15px;
}

.gallery-theme {
  margin-bottom: 20px;
}
</style>
