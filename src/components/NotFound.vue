<script setup>

const props = defineProps({
  term: String
});

</script>

<template>
  <h1>Oops!</h1>
  <p>
    We searched for <span class="term">"{{props.term.replace('_', ' ')}}"</span> North, South, East, and West. It ought to be somewhere, but it is not here!
  </p>
</template>

<style scoped>
.term {
  text-transform: capitalize;
}
</style>
