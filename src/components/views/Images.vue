<template>
  <div class="images">
    <section>
      <div class="frame" @click="$emit('selected-image', images)">
        <img v-bind:src="images.primaryimageurl" />
      </div>
    </section>
  </div>
</template>

<script>
export default {
  name: "Images",
  props: ["images"]
};
</script>
<style scoped>
.images {
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
  /* margin: 10vh 10vw; */
  height: 40vh;
  position: relative;
  text-align: center;
  cursor: pointer;
  margin: 0;
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
</style>
