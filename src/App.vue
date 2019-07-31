<template>
  <div id="app">
    <Header v-on:return-btn="openGallerySlides"/>
    <Gallery
      v-bind:class="{'slideshow-on':(selectedGalleryId === ''), 'slideshow-off':(selectedGalleryId !== '')}"
      v-bind:galleryInfo="galleryInfo"
      v-on:selected-gallery="selectedGallery"
    />
    <Images
      v-on:selected-image="selectedImage"
      v-on:return-btn="openGallerySlides"
      v-if="gallerySelected"
      v-bind:galleryId="selectedGalleryId"
    />
    <ImageModal
      v-bind:currentImage="currentImage"
      v-if="noSelectedImages"
      v-on:close-modal="closeModal"
    />
  </div>
</template>

<script>
import Header from "./components/views/Header";
import Images from "./components/views/Images";
import ImageModal from "./components/views/ImageModal";
import Gallery from "./components/views/Gallery";
import galleryArray from "./helper/data";
import axios from "axios";

export default {
  name: "app",
  components: {
    Header,
    Images,
    ImageModal,
    Gallery
  },
  data() {
    return {
      currentImage: [],
      selectedGalleryId: "",
      galleryInfo: []
    };
  },
  methods: {
    selectedImage(image) {
      this.currentImage = [image];
    },
    closeModal() {
      this.currentImage = [];
    },
    selectedGallery(id) {
      this.selectedGalleryId = id;
    },
    openGallerySlides() {
      this.selectedGalleryId = "";
    }
  },
  computed: {
    noSelectedImages() {
      return this.currentImage.length >= 1;
    },
    gallerySelected() {
      return this.selectedGalleryId !== "";
    }
  },
  created() {
    this.galleryInfo = galleryArray;
  }
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: Arial, Arial, Helvetica, sans-serif;
  line-height: 1.4;
  background: url(assets/gallery.jpg) no-repeat center center fixed;
  -webkit-background-size: cover;
  -moz-background-size: cover;
  -o-background-size: cover;
  background-size: cover;
}

.btn {
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}

.btn:hover {
  background: #666;
}

.slideshow-on {
  height: 89vh;
  transition: all 1.5s ease 1.5ms;
}

.slideshow-off {
  height: 0vh;
  transition: all 1.5s ease 1.5ms;
}
</style>
