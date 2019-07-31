<template>
  <div class="images">
    <loading
      :active.sync="this.isLoading"
      :is-full-page="true"
    ></loading>
    <div class="btn-area" id="nav1" @click="$emit('return-btn')">
      <h2>
        <img
          class="nav-icon"
          src="https://i.imgur.com/P7L54S6.png"
          alt="folder with plus sign on it."
        />
        Return To Galleries
      </h2>
    </div>
    <section v-bind:key="image.id" v-for="image in images">
      <div class="frame" @click="$emit('selected-image', image)">
        <img v-bind:src="image.primaryimageurl" />
      </div>
    </section>
  </div>
</template>

<script>
import axios from "axios";
import Loading from "vue-loading-overlay";
import "vue-loading-overlay/dist/vue-loading.css";

export default {
  name: "Images",
  props: ["galleryId"],
  data() {
    return {
      images: [],
      currentImage: {},
      isLoading: false
    };
  },
  components: {
    Loading
  },
  created() {
    this.isLoading = true;
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
      .then(this.isLoading = false)
      .catch(error => console.log(error));
  }
};
</script>
<style scoped>
.images {
  display: grid;
  grid-template-columns: 1fr 1fr;
  padding: 50px;
}

img {
  height: 250px;
  width: 250px;
  padding: 30px 30px 45px 30px;
}

.frame {
  background-color: #ddc;
  border: solid 5vmin #eee;
  border-bottom-color: #fff;
  border-left-color: #eee;
  border-radius: 2px;
  border-right-color: #eee;
  border-top-color: #ddd;
  box-shadow: 0 0 5px 0 rgba(0, 0, 0, 0.25) inset,
    0 5px 10px 5px rgba(0, 0, 0, 0.25);
  box-sizing: border-box;
  display: inline-block;
  margin: 10vh 10vw;
  height: 40vh;
  position: relative;
  text-align: center;
  cursor: pointer;
}

.frame:before {
  border-radius: 2px;
  bottom: -2vmin;
  box-shadow: 0 2px 5px 0 rgba(0, 0, 0, 0.25) inset;
  content: "";
  left: -2vmin;
  position: absolute;
  right: -2vmin;
  top: -2vmin;
}

.frame:after {
  border-radius: 2px;
  bottom: -2.5vmin;
  box-shadow: 0 2px 5px 0 rgba(0, 0, 0, 0.25);
  content: "";
  left: -2.5vmin;
  position: absolute;
  right: -2.5vmin;
  top: -2.5vmin;
}

.btn-area {
  background-color: #10b0ee;
  width: 300px;
  height: 60px;
  border-radius: 30px;
  position: fixed;
  right: -230px;
  transition: 0.8s ease;
  box-shadow: 4px 5px 10px #000;
  cursor: pointer;
}

.btn-area:hover {
  background-color: #262626;
  position: fixed;
  right: -50px;
  width: 300px;
  border: none;
  color: #fff;
  border-radius: 0;
}

.nav-icon {
  height: 100px;
  width: 100px;
  z-index: 999;
}

h2 img {
  position: absolute;
  left: -15px;
  bottom: 0px;
  color: #fff;
  font-size: 25px !important;
  padding-top: 4px;
  top: -17px;
}

h2 {
  font-family: baloo;
  font-weight: bold;
  position: relative;
  top: 20px;
  text-align: center;
  left: 5px;
  font-size: 20px;
}

#nav1 {
  top: 100px;
}
</style>
