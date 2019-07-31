<template>
  <div class="modal-mask">
    <div class="modal-wrapper" v-bind:key="image.id" v-for="image in currentImage">
      <div class="modal-container">
        <div class="modal-info">
          <div>
            <img class="modal-image" v-bind:src="image.primaryimageurl" />
          </div>
          <div class="modal-content">
            <img
              class="close-icon"
              src="https://i.imgur.com/iSC7dNW.png"
              alt="folder with plus sign on it."
              @click="$emit('close-modal')"
            />
            <div class="modal-header">
              <p class="modal-label">Title</p>
              <slot name="header">{{image.title}}</slot>
            </div>
            <div class="modal-body">
              <p class="modal-label">Century</p>
              <slot name="body">{{image.dated}} / {{image.century}}</slot>
            </div>
            <div class="modal-body">
              <p class="modal-label">Culture</p>
              <slot name="body">{{image.culture}}</slot>
            </div>
            <p class="modal-label">Description</p>
            <div class="modal-description">
              <slot name="body">{{image.labeltext}}</slot>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ImageModal",
  props: ["currentImage"]
};
</script>

<style>
.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: table;
  transition: opacity 0.3s ease;
}

.modal-label {
  color: #999;
}

.modal-description {
  max-height: 150px;
  overflow: scroll;
}

.modal-wrapper {
  display: table-cell;
  vertical-align: middle;
}

.modal-info {
  display: flex;
}

.modal-content {
  padding: 20px;
  min-width: 415px;
}

.modal-container {
  width: 800px;
  margin: 0px auto;
  padding: 20px 30px;
  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
  transition: all 0.3s ease;
  font-family: Helvetica, Arial, sans-serif;
}

.modal-header h3 {
  margin-top: 0;
  color: #42b983;
}

.modal-body {
  margin: 20px 0;
}

.modal-image {
  height: 400px;
  width: 350px;
}

.modal-default-button {
  float: right;
  cursor: pointer;
}

.modal-enter {
  opacity: 0;
}

.modal-leave-active {
  opacity: 0;
}

.modal-enter .modal-container,
.modal-leave-active .modal-container {
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}

.close-icon {
  height: 10%;
  width: 10%;
  float: right;
  cursor: pointer;
  padding-bottom: 10px;
}
</style>
