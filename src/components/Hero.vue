<script setup>
const props = defineProps({
  background: String
});

const backgroundImage = {
  "backgroundImage" :  `url('${require('../assets/the_church.png')}')`
}

</script>

<template>
  <div class="hero" :style="backgroundImage">
    <slot/>
  </div>
</template>

<style>
.hero {
  width: 100%;
  aspect-ratio: 1140 / 468 ;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  background-repeat: no-repeat;
  background-size: cover;
  text-align: center;
}
</style>
