<template>
  <div class="gallery-slides">
    <div @mouseover="isHovering = true" @mouseout="isHovering = false">
      <li @click="$emit('selected-gallery', galleryInfo.id)">
        <div v-bind:class="{'not-caption':(isHovering === false), 'caption':(isHovering === true)}">
          <a href="#">{{galleryInfo.name}}</a>
          <a class="gallery-theme" href="#">{{galleryInfo.theme}}</a>
        </div>
        <a href="#">
          <img v-bind:src="galleryInfo.image" />
        </a>
      </li>
    </div>
  </div>
</template>

<script>
export default {
  name: "GallerySlides",
  props: ["galleryInfo"],
  data() {
    return {
      isHovering: false
    };
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
