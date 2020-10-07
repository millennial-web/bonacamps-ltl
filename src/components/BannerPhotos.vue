<template>
  <div class="main_banner_wrapper">
      <a class="prev-button" @click="prevSlide()">
        &lt;
      </a>
      <a class="next-button" @click="nextSlide()">
        &gt;
      </a>
      <transition appear name="banner" v-on:after-enter="BannerAfterEnter">
      <div v-if="show_banner" class="main-banner" :style="{ backgroundImage: 'url(' + require('@/assets/imgs/'+slide_data[current_slide].image) + ')' }">
        
        <transition name="fade" v-on:after-enter="TextContainerAfterEnter">
          <div v-if="show_text_container"  class="banner-text-container">
            <transition name="fade" v-on:after-enter="TitleAfterEnter">
              <div v-if="show_title" class="title-text">
                {{ slide_data[current_slide].title }}
              </div>
            </transition>
            <transition name="fade" v-on:after-enter="SubtitleAfterEnter">
              <div v-if="show_subtitle" class="subtitle-text">
                {{ slide_data[current_slide].subtitle }}
                <p class="description-text">
                  {{ slide_data[current_slide].description }}
                </p>
              </div>
            </transition>
          </div>
        </transition>

      </div>
    </transition>
  </div>
  
</template>

<script>

export default {
  name: 'BannerPhotos',
  data: function () {
      return {
          current_slide: 0,
          auto_change_started:false,
          slide_data: [
            { 
              image: 'truck-back-view.jpeg', 
              title: 'BONACAMPS LTL', 
              subtitle: 'Less than truckload freight shipping services', 
              description: 'Transportation of small freight between 100 to 1000 lbs.',
            },
            { 
              image: 'forklift-slide.jpg', 
              title: 'BONACAMPS LTL', 
              subtitle: 'Benefits of shipping LTL', 
              description: 'Reduced cost, Freight Tracking, Increased Security',
            },
            { 
              image: 'truck-driver.jpeg', 
              title: 'BONACAMPS LTL', 
              subtitle: '+10 years experienced driver', 
              description: '6ftx12ft enclosed trailer & Tundra truck',
            },
            { 
              image: 'us-map.jpg', 
              title: 'BONACAMPS LTL', 
              subtitle: 'Long run over southernmost states.', 
              description: 'Arizona. New Mexico, Lousiana, Georgia, Florida (base @ Dallas Texas)',
            },
          ],
          show_banner: true,
          show_text_container: false,
          show_title: false,
          show_subtitle: false,
          anims_done: false,
      }
  },
  created: function(){
    this.current_slide = 0;
  },
  methods: {
    nextSlide: function(){
      if(this.anims_done){
        this.anims_done = false;
        this.show_banner = false;
        this.show_text_container = false;
        this.show_title = false;
        this.show_subtitle = false;
        this.anims_done = false;

        setTimeout(function(){
          if(this.current_slide +1 < this.slide_data.length){
            this.current_slide+= 1;
          }else{
            this.current_slide = 0;
          }
          this.show_banner = true;
        }.bind(this), 400);
      }
    },
    BannerAfterEnter: function(){
      this.show_text_container = true;
    },
    TextContainerAfterEnter: function(){
      this.show_title = true;
    },
    TitleAfterEnter: function(){
      this.show_subtitle = true;
    },
    SubtitleAfterEnter: function(){
      this.anims_done = true;
      // if(!this.auto_change_started){
      //   setInterval(function(){ 
      //       this.auto_change_started = true;
      //       nextSlide();
      //   }, 3000);
      // }
    },

  },
  components: {

  }
}
</script>

<style scoped>
.main_banner_wrapper{
  min-height:560px;
  background-color:#777;
  overflow: hidden;
}
.main-banner{
  background-size:cover;
  background-repeat:no-repeat;
  height:500px;
  background-position:center right;
  padding-top:60px;
}
.banner-text-container{
  margin:0 0 0 100px;
  padding:40px;
  background-color:rgba(32, 129, 153, 0.8);
  max-width:20%;
  border-radius:10px;
  box-shadow:2px 2px 15px #333;
  border: 1px solid #333;
  min-height:25vh;
}
.title-text{
  text-align:center;
  padding:10px auto;
  margin:0;
  color:aliceblue;
  font-size:30px;
  font-family: 'Anton', sans-serif;
}
.subtitle-text{
  text-align:center;
  margin:10px auto 0px auto;
  color:aliceblue;
  font-size:20px;
  font-weight:normal;
  font-family: 'Anton', sans-serif;
}
.description-text{
  font-family:Arial, Helvetica, sans-serif;
  font-size:16px;
  margin:30px auto 0px auto;
}
a.next-button{
  position:absolute;
  top:35%;
  right:20px;
  display:block;
  margin:0;
  padding:0px;
  line-height: 42px;
  font-family: 'Anton', sans-serif;
  font-size:85px;
  font-weight:bold;
  color:rgb(20,20,20,0.9);
  text-align:right;
  width:30px;
  height:50px;
} 
a.next-button:hover{
  cursor:pointer;
}
a.prev-button{
  position:absolute;
  top:35%;
  left:20px;
  display:block;
  margin:0;
  padding:0px;
  line-height: 42px;
  font-family: 'Anton', sans-serif;
  font-size:85px;
  font-weight:bold;
  color:rgb(20,20,20,0.9);
  text-align:right;
  width:30px;
  height:50px;
} 
a.prev-button:hover{
  cursor:pointer;
}

/* ======= transitions ======== */
.banner-enter-active{
  transition: all .3s ease-in-out;
} 
.banner-leave-active {
  transition: all .2s ease-in-out;
}
.banner-enter{
  opacity: 0;
  transform: translateX(400px);
}
.banner-leave-to {
  opacity: .5;
  transform: translateX(-400px);
}
.fade-enter-active, .fade-leave-active {
  transition: all .3s;
  opacity:.5;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
  transform: translateX(100px);
}

@media only screen and (max-width: 1000px) {
  .main_banner_wrapper{
    height:200px;
    min-height:200px;
  }
  .main-banner{
    height:200px;
    padding-top:20px;
  }
  .banner-text-container{
    margin:0 auto;
    padding:10px;
    max-width:70%;
    min-height:150px;
  }
  .title-text{
    padding:10px auto;
    font-size:22px;
  }
  .subtitle-text{
    text-align:center;
    margin:10px auto 0px auto;
    color:aliceblue;
    font-size:16px;
  }
  .description-text{
    font-family:Arial, Helvetica, sans-serif;
    font-size:14px;
    margin:20px auto 0px auto;
  }
  a.next-button{
    top:90px;
    right:15px;
    line-height:22px;
    font-size:45px;
  } 
  a.prev-button{
    top:90px;
    left:15px;
    line-height: 22px;
    font-family: 'Anton', sans-serif;
    font-size:45px;
  } 
}

</style>
