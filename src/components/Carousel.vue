<template>
  <div>
    <div class="carousel">
      <slot :currentSlider="currentSlider" />
    </div>
    <div v-if="navEnabled" class="navigation">
      <div class="toggle-page left">
        <div @click="prevSlider" class="icon-container">
          <i class="fa-solid fa-chevron-left"></i>
        </div>
      </div>
      <div class="toggle-page right">
        <div @click="nextSlider" class="icon-container">
          <i class="fa-solid fa-chevron-right"></i>
        </div>
      </div>
    </div>
    <div v-if="paginationEnabled" class="pagination">
      <span
        @click="goToSlide(index)"
        v-for="(slider, index) in getSliderCount"
        :key="index"
        :class="{ active: index + 1 === currentSlider }"
      ></span>
    </div>
  </div>
</template>

<script>
import { ref, onMounted } from 'vue';

export default {
  props: ['startAutoPlay', 'timeout', 'navigation', 'pagination'],
  setup(props) {
    const currentSlider = ref(1);
    const getSliderCount = ref(null);
    const autoPlayEnabled = ref(
      props.startAutoPlay === undefined ? true : props.startAutoPlay
    );
    const timeoutDuration = ref(
      props.timeout === undefined ? 5000 : props.timeout
    );
    const paginationEnabled = ref(
      props.pagination === undefined ? true : props.pagination
    );
    const navEnabled = ref(
      props.navigation === undefined ? true : props.navigation
    );

    const nextSlider = () => {
      const totalSlides = getSliderCount.value;

      if (currentSlider.value === totalSlides) {
        currentSlider.value = 1;
      } else
      currentSlider.value += 1;
    };

    const prevSlider = () => {
      const totalSlides = getSliderCount.value;

      if (currentSlider.value === 1) {
        currentSlider.value = totalSlides;
      } else
      currentSlider.value -= 1;
    };

    const goToSlide = (index) => {
      currentSlider.value = index + 1;
    };

    const autoPlay = () => {
      setInterval(() => {
        nextSlider();
      }, timeoutDuration.value);
    };

    if (autoPlayEnabled.value) {
      autoPlay();
    }

    onMounted(() => {
      getSliderCount.value = document.querySelectorAll('.slider').length;
    });

    return {
      currentSlider,
      nextSlider,
      prevSlider,
      getSliderCount,
      goToSlide,
      paginationEnabled,
      navEnabled
    };
  }
};
</script>

<style>
.navigation {
  position: absolute;
  height: 100%;
  width: 100%;
  padding: 0 16px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.toggle-page {
  display: flex;
  flex: 1;
}

.right {
  justify-content: flex-end;
}

.icon-container {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 40px;
  height: 40px;
  background-color: rgb(113, 13, 180);
  color: #fff;
  border-radius: 50%;
  cursor: pointer;
}

.pagination {
  position: absolute;
  bottom: 24px;
  display: flex;
  gap: 16px;
  justify-content: center;
  align-items: center;
  width: 100%;
}

span {
  width: 20px;
  height: 20px;
  border-radius: 50%;
  cursor: pointer;
  background-color: #fff;
  box-shadow:
    0 1px 3px 0 rgba(0, 0, 0, 0.1),
    0 1px 2px 0 rgba(0, 0, 0, 0.06);
}

.active {
  background-color: rgb(113, 13, 180);
}
</style>
