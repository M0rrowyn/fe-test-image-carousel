<template>
  <div class="slider">
    <transition name="slider">
      <slot />
    </transition>
  </div>
</template>

<script></script>

<style>
.slider-enter-active,
.slider-leave-active {
  transition: opacity 0.7s ease-in-out;
}

.slider-enter-from,
.slider-leave-to {
  opacity: 0;
}

.slider-enter-to,
.slider-leave-from {
  opacity: 1;
}
</style>
