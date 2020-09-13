<template>
  <div id="app">
    <BannerPhotos></BannerPhotos>
    <WhatIsLTL></WhatIsLTL>
  </div>
</template>

<script>
import WhatIsLTL from './components/WhatIsLTL.vue'
import BannerPhotos from './components/BannerPhotos.vue'

export default {
  name: 'App',
  components: {
    BannerPhotos,
    WhatIsLTL,
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Anton&display=swap');

  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 0px;
  }

</style>
