<script setup>
import { RouterLink, RouterView } from "vue-router";
</script>

<template>
  <RouterView />

  <div id="bg">
    <lottie-player
      class="back"
      src="https://assets2.lottiefiles.com/packages/lf20_82kLQImg0d.json"
      background="transparent"
      speed="1"
      loop
      style="width: 100vw; height: auto"
      autoplay
    ></lottie-player>
  </div>
</template>

<style scoped>
#bg {
  background-color: black;
  display: flex;
  justify-content: center;
  align-items: center;
  position: fixed;
  top: 0;
  right: 0;
  width: 100vw;
  height: 100vh;
  z-index: -1;
}
</style>
