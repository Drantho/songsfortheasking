<script setup>

import { useRoute } from "vue-router";
import data from "app/newData";
import NotFound from "src/components/NotFound.vue";

const route = useRoute();

const bandId = route.params.bandId;
const albumId = route.params.albumId;
const songId = route.params.songId;

const band = data.find(band => band.bandId === bandId);
const album = band.albums.find(album => album.albumId === albumId);
const song = album.tracks.find(song => song.titleId === songId);

</script>

<template>

<template v-if="band && album && song">
<h1>
{{song.title}} - {{band.band}}
</h1>
<h2>
  {{song.credit.join(", ")}}
</h2>
<h3 v-if="song.transcribed">
  transcribed by {{song.transcribed.join(", ")}}
</h3>

<div v-if="song.listen" v-html="song.listen">

</div>
<pre>
  {{song.song}}
</pre>
</template>

<template v-else>
<NotFound :term="`${bandId} - ${albumId} - ${songId}`"/>
</template>

</template>

<style scoped>

</style>
