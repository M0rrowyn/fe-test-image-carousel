<template>
  <div>
    <div class="carousel">
      <slot :currentSlider="currentSlider" />
    </div>
    <div class="navigation">
      <div class="toggle-page left">
        <div class="icon-container">
          <i @click="prevSlider" class="fa-solid fa-chevron-left"></i>
        </div>
      </div>
      <div class="toggle-page right">
        <div class="icon-container">
          <i @click="nextSlider" class="fa-solid fa-chevron-right"></i>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, onMounted } from 'vue';
export default {
  setup() {
    const currentSlider = ref(1);
    const getSliderCount = ref(null);

    const nextSlider = () => {
      if (currentSlider.value === getSliderCount.value) {
        currentSlider.value = 1;
        return;
      }
      currentSlider.value += 1;
    };

    const prevSlider = () => {
      if (currentSlider.value === 1) {
        currentSlider.value = 1;
        return;
      }
      currentSlider.value -= 1;
    };

    onMounted(() => {
      getSliderCount.value = document.querySelectorAll('.slider').length;
    });

    return { currentSlider, nextSlider, prevSlider };
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
</style>