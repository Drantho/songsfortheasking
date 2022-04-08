<script setup>

import { useRoute } from "vue-router";
import data from "app/newData";
import NotFound from "src/components/NotFound.vue";

const route = useRoute();

const bandId = route.params.bandId
const albumId = route.params.albumId

const band = data.find(band => band.bandId === bandId);
const album = band.albums.find(album => album.albumId === albumId);

</script>

<template>

<template v-if="band && album">
<h1>
{{album.album}} - {{band.band}}
</h1>

<img :src="album.cover" :alt="`${album.album} photo`">

<h2>listen</h2>
<div v-html="album.listen"></div>

<h2>tracks</h2>
<ul>
  <li v-for="song in album.tracks" :key="song.titleId">
    <RouterLink :to="`/song/${bandId}/${albumId}/${song.titleId}`">
      {{song.title}}
    </RouterLink>
  </li>
</ul>

</template>

<template v-else>
<NotFound :term="`${bandId} - ${albumId}`"/>
</template>

</template>

<style scoped>

</style>
