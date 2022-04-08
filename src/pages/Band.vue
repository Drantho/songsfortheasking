<script setup>

import { useRouter, useRoute, RouterLink } from "vue-router";
import data from "app/newData";
import NotFound from "src/components/NotFound.vue";

const router = useRouter();
const route = useRoute();

const bandId = route.params.bandId
const band = data.find(band => band.bandId === bandId);

</script>

<template>

<template v-if="band">
<h1>
  {{band.band }}
</h1>

<img :src="require(`../assets/${band.image}`)" :alt="`${band.band} photo`">
<p>
  {{band.info.text}} - {{band.info.attribution}}
</p>

 <h2>Links</h2>
<template v-if="band.links.official">
  <h3>official</h3>
 <ul>
   <li v-for="link in band.links.official" :key="link.name">
     <a :href="link.url" target="_blank">{{link.name}}</a>
   </li>
 </ul>
</template>
<template v-if="band.links.info">
  <h3>info</h3>
 <ul>
   <li v-for="link in band.links.info" :key="link.name">
     <a :href="link.url" target="_blank">{{link.name}}</a>
   </li>
 </ul>
</template>
<template v-if="band.links.listen">
  <h3>listen</h3>
 <ul>
   <li v-for="link in band.links.listen" :key="link.name">
     <a :href="link.url" target="_blank">{{link.name}}</a>
   </li>
 </ul>
</template>
<template v-if="band.links.fan">
  <h3>fan</h3>
 <ul>
   <li v-for="link in band.links.fan" :key="link.name">
     <a :href="link.url" target="_blank">{{link.name}}</a>
   </li>
 </ul>
</template>
<h2>Albums</h2>
<ul>
  <li v-for="album in band.albums" :key="album.albumId">
  <RouterLink :to="`/album/${band.bandId}/${album.albumId}`">
    {{album.album}}
  </RouterLink>
    <ul>
      <li v-for="song in album.tracks" :key="song.titleId">
        {{song.title}}
      </li>
    </ul>
  </li>
</ul>
</template>

<template v-else>
<NotFound :term="bandId"/>
</template>

</template>

<style scoped>

</style>
