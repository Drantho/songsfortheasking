<script setup>
import data from 'app/newData';

  const props = defineProps({
    songId: {
      type: String,
    },
    albumId: {
      type: String,
    },
    bandId: {
      type: String,
    },
  });

  const band = data.find(band => band.bandId === props.bandId);
  const album = props.albumId ? band.albums.find(album => album.albumId === props.albumId) : undefined;
  const song = props.songId ? album.tracks.find(song => song.titleId === props.songId) : undefined;

</script>

<template>
  <div class="q-pa-md q-gutter-sm breadcrumb">
    <q-breadcrumbs>

      <q-breadcrumbs-el icon="home" to="/" />

      <template v-if="props.bandId">
        <q-breadcrumbs-el :label="band.band" :to="`/band/${bandId}`" v-if="props.albumId"/>
        <q-breadcrumbs-el :label="band.band" v-else/>
      </template>

      <template v-if="props.albumId">

        <q-breadcrumbs-el :label="album.album" :to="`/album/${bandId}/${albumId}`"  v-if="props.songId"/>
        <q-breadcrumbs-el :label="album.album"  v-else/>

      </template>

      <q-breadcrumbs-el :label="song.title" v-if="props.songId"/>



    </q-breadcrumbs>
  </div>
</template>

<style>
.breadcrumb {
  position: absolute;
  top: 75px;
}

span.q-breadcrumbs__el {
  font-weight: 700;
}

a.q-breadcrumbs__el {
  font-weight: 400;
}

</style>
