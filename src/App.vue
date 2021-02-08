<template>
  <div id="app">
    <div class="gallery" v-click-outside="outside" @click="inside">
      <div
        v-for="(img, idx) in imgs"
        :key="idx"
        class="pic"
        @click="() => show(idx)"
      >
        <img :src="img.src ? img.src : img" style="width: 250px; height: 250px;">
      </div>
    </div>

    <vue-easy-lightbox
      :visible="visible"
      :index="index"
      :imgs="imgs"
      @hide="visible = false"
    />
  </div>
</template>

<script>
  import VueEasyLightbox from 'vue-easy-lightbox'
  import say from 'sweetalert'

  export default {
    name: 'App',
    components: {
      VueEasyLightbox
    },
    data() {
      return {
        imgs: [
          'https://user-images.githubusercontent.com/69447666/107151776-bc079300-69a7-11eb-9de6-8f1f5cc60ec5.jpg',
          'https://user-images.githubusercontent.com/69447666/107151777-bd38c000-69a7-11eb-93c2-98bc2a19eba5.jpg',
          'https://user-images.githubusercontent.com/69447666/107151778-be69ed00-69a7-11eb-8fcb-9eea9e3629e4.jpg',
          'https://user-images.githubusercontent.com/69447666/107151777-bd38c000-69a7-11eb-93c2-98bc2a19eba5.jpg',
          'https://user-images.githubusercontent.com/69447666/107151776-bc079300-69a7-11eb-9de6-8f1f5cc60ec5.jpg',
          'https://user-images.githubusercontent.com/69447666/107151776-bc079300-69a7-11eb-9de6-8f1f5cc60ec5.jpg',
        ],
        visible: false,
        index: 0,
        messages: "Press image",
        first: false
      }
    },
    methods: {
      show(index) {
        this.index = index
        this.visible = true
        this.first = false
      },
      outside() {
         console.log('clicked outside');
         if(!this.first){
            say(this.messages);
            this.first = true
         }
      },
      inside() {
        console.log('clicked inside!');
      }
    }
  }
</script>

<style>
  #app {
    margin: 15%;
  }

  .gallery {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    grid-gap: 50px;
    align-items: center;
    justify-content: center;
  }

  .pic {
    cursor: pointer;
  }
</style>