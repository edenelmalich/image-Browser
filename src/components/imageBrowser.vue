<template>
  <div class="imageBrowser">
    <header>
      <div class="header-text">Image Browser</div>
    </header>
    <div class="Search-att">
      <input type="text" placeholder="Search Image..." v-model="tag" />
      <input type="submit" @click.prevent="getImages" value="Search" />
    </div>
    <div class="Container-images">
      <div v-for="image in images" v-bind:key="image.id">
        <a href="#">
          <img
            class="image-box"
            :src="image.url_n"
            :alt="image.title"
            @click.prevent="OpenModal(image.url_n)"
          />
        </a>
      </div>
      <div v-if="modal" class="Modal-Container">
        <div @click.prevent="modal=false" class="CloseModal">+</div>
        <div @click.prevent="modal=false" class="Moda-box">
          <img :src="UrlModal" />
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import axios from "axios";
import { Component, Prop, Vue } from "vue-property-decorator";
export default Vue.extend({
  name: "imageBrowser",
  data() {
    return {
      images: [],
      tag: " ",
      modal: false,
      UrlModal: " "
    };
  },
  methods: {
    // This function call to the server to get the images with axios
    getImages: function() {
      return axios({
        method: "get",
        url: "https://api.flickr.com/services/rest",
        params: {
          method: "flickr.photos.search",
          api_key: "762691a97bd7b7387c07c53e860579ad",
          format: "json",
          extras: "url_n",
          tags: this.tag,
          nojsoncallback: 1,
          per_page: 500
        }
      })
        .then(res => {
          this.images = res.data.photos.photo;
        })
        .catch(error => {
          console.log("Error", error);
        });
    },
    // This function change the modal state and put the url in the UrlModal state
    OpenModal: function(Imageurl) {
      if (this.modal) {
        this.modal = false;
      } else {
        this.modal = true;
        this.UrlModal = Imageurl;
      }
    }
  },
  // This function connect the flicker server and push the images in images state.
  created() {
    this.getImages();
  }
});
</script>

<style lang="scss">
.Moda-box {
  position: absolute;
  width: 300px;
  height: 300px;
  z-index: 3;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
}
.Modal-Container {
  position: absolute;
  height: 100%;
  width: 100%;
  z-index: 3;
  top: 0;
  display: flex;
  background-color: rgba(0, 0, 0, 0.7);
  justify-content: center;
}
.CloseModal {
  position: absolute;
  top: 20%;
  right: 25%;
  color: #ffffff;
  font-size: 50px;
  transform: rotate(45deg);
  cursor: pointer;
}
</style>