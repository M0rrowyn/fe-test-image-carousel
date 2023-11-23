<template>
  <div class="app">
    <Carousel class="carousel">
      <Slider v-for="(slider, index) in carouselSliders" :key="index">
        <div class="slider-info">
          <img class="slider-img" :src="slider" />
        </div>
      </Slider>
    </Carousel>
  </div>
</template>

<script>
import Carousel from './components/Carousel.vue';
import Slider from './components/Slider.vue';

export default {
  name: 'App',
  components: {
    Carousel,
    Slider
  },
  setup() {
    const carouselSliders = [
      'https://picsum.photos/id/119/900/400',
      'https://picsum.photos/id/149/900/400',
      'https://picsum.photos/id/237/900/400',
      'https://picsum.photos/id/429/900/400',
      'https://picsum.photos/id/593/900/400'
    ];
    return { carouselSliders };
  }
};
</script>

<style scoped>
.carousel {
  position: relative;
  max-height: 100vh;
  height: 100vh;
}

.slide-info {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  max-height: 100%;
  height: 100%;
}

.slider-img {
  min-width: 100%;
  height: 100%;
  object-fit: cover;
}
</style>
