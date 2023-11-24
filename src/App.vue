<template>
  <div class="app">
    <Carousel
      :navigation="true"
      :pagination="true"
      :startAutoPlay="false"
      class="carousel"
      v-slot="{ currentSlider }"
    >
      <Slider v-for="(slider, index) in carouselSliders" :key="index">
        <div v-if="currentSlider === index + 1" class="slider-info">
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
      'https://picsum.photos/id/119/800/400',
      'https://picsum.photos/id/149/800/400',
      'https://picsum.photos/id/237/800/400',
      'https://picsum.photos/id/429/800/400',
      'https://picsum.photos/id/593/800/400',
      'https://picsum.photos/id/152/800/400'
    ];
    return { carouselSliders };
  }
};
</script>

<style scoped>
.app {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background-color: #f0f0f0;
}
.app {
  display: flex;
  justify-content: center;
  align-items: center;
}
.carousel {
  position: relative;
  width: 800px;
  height: 400px;
  overflow: hidden;
}

.slider-info {
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
