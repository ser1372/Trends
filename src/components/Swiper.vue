
<template>
  <swiper
    :slides-per-view="3"
    :space-between="50"
    @swiper="onSwiper"
    @slideChange="onSlideChange"
  >
    <swiper-slide><img src = "../assets/layouts/images/prop5.png" class="properties__img__swiper"></swiper-slide>
    <swiper-slide><img src = "../assets/layouts/images/prop2.png" class="properties__img__swiper"></swiper-slide>
    <swiper-slide><img src = "../assets/layouts/images/prop4.png" class="properties__img__swiper"></swiper-slide>
    ...
  </swiper>
</template>
<script>
  // Import Swiper Vue.js components
  import { Swiper, SwiperSlide } from 'swiper/vue';

  // Import Swiper styles
  import 'swiper/css';

  export default {
    components: {
      Swiper,
      SwiperSlide,
    },
    setup() {
      const onSwiper = (swiper) => {
        console.log(swiper);
      };
      const onSlideChange = () => {
        console.log('slide change');
      };
      return {
        onSwiper,
        onSlideChange,
      };
    },
  };
</script>






<style lang = "scss">

.home{
    &__carousel-indicators{
    bottom: 200px;
}
}

.carousel__img{
  max-width: 2000px;
  max-height: 1000px;
}



.swiper{
  max-width: 100%;
  max-height: 100%;
}

.img__style{
  max-width: 2000px;
  max-height: 1000px;
}


</style>




