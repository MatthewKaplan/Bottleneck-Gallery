<template>
  <div class="gallery-description">
    <div class="gallery-info">
      <h1>{{currentGalleryInfo[0].name}}</h1>
      <h3>{{currentGalleryInfo[0].theme}}</h3>
      <hr />
      <section>
        <p>{{currentGalleryInfo[0].description}}</p>
      </section>
    </div>
  </div>
</template>

<script>
export default {
  name: "GalleryDescription",
  props: ["galleryId", "galleryInfo"],
  data() {
    return {
      currentGalleryInfo: null
    };
  },
  created() {
    this.currentGalleryInfo = this.galleryInfo.galleryArray.filter(gallery => {
      return gallery.id === this.galleryId;
    });
  }
};
</script>

<style>
.gallery-info {
  border: 2px solid white;
  background: rgba(124, 119, 119, 0.8);
  max-height: 87.5vh;
  padding: 10px;
}

.gallery-info section {
  max-height: 69vh;
  overflow: scroll;
}
</style>
