<script setup>
import { useRoute } from "vue-router";
import data from "app/newData";
import { ref } from "vue";
import NotFound from "src/components/NotFound.vue";

const route = useRoute();

const bandId = route.params.bandId;
const albumId = route.params.albumId;
const songId = route.params.songId;

const band = data.find((band) => band.bandId === bandId);
const album = band.albums.find((album) => album.albumId === albumId);
const song = album.tracks.find((song) => song.titleId === songId);

let tab = ref('play')
</script>

<template>
  <template v-if="band && album && song">
    <h2>
      {{ song.title }}<br/>
      {{ band.band }}
    </h2>
    <h3>
      ({{ song.credit.join(", ") }})
    </h3>
    <h4 v-if="song.transcribed">
      transcribed by {{ song.transcribed.join(", ") }}
    </h4>

    <q-card>
      <q-tabs
        v-model="tab"
        dense
        class="text-grey"
        active-color="primary"
        indicator-color="primary"
        align="justify"
        narrow-indicator
      >
        <q-tab name="play" label="Play" />
        <q-tab name="listen" label="Listen" />
      </q-tabs>

      <q-separator />

      <q-tab-panels v-model="tab" animated>
        <q-tab-panel name="play">
          <pre>
            {{ song.song }}
          </pre>
        </q-tab-panel>
        <q-tab-panel name="listen">
          <div v-if="song.listen" v-html="song.listen"></div>
        </q-tab-panel>
      </q-tab-panels>
    </q-card>
  </template>

<template v-else>
  <NotFound :term="`${bandId} - ${albumId} - ${songId}`" />
</template>
</template>


<style scoped>
</style>
