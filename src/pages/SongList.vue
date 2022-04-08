<script setup>
import data from "../../newData";
import { RouterLink, RouterView } from "vue-router";

let songs = [];
const alphabet = ['a','b','c','d','e','f','g','h','i','j','k','l','m','n','o','p','q','r','s','t','u','v','w','x','y','z'];
for(let i=0; i<26; i++) {
  songs.push({title: alphabet[i]});
}
data.forEach((band) => {
  band.albums.forEach((album) => {
    album.tracks.forEach((track) => {
      songs.push({ ...track, album: album, band: band });
    });
  });
});

songs = songs.sort((a, b) => {
  if (a.title.toLowerCase() > b.title.toLowerCase()) {
    return 1;
  } else if (a.title.toLowerCase() < b.title.toLowerCase()) {
    return -1;
  }
  return 0;
});
console.log("songs: ", songs);

const scrollTo = item => {
  console.log('item: ', item);
  const element = document.querySelector('#' + item);
  window.scrollTo({
    left: 0,
    top: element.offsetTop,
    behavior: 'smooth'
    })
}
</script>

<template>
  <q-page>
    <h1>Song List</h1>
    <span v-for="item in alphabet" :key="item">
      <a class="capitalize" @click="scrollTo(item)">{{item}}</a><span v-if="item !== 'z'"> | </span>
    </span>
    <ul id="songlist">
      <li v-for="item in songs" :key="item.title">

          <template  v-if="item.titleId">
            <RouterLink :to="`/song/${item.band.bandId}/${item.album.albumId}/${item.titleId}`">
              {{item.title}}
            </RouterLink>
          </template>
        <span :id="item.title" v-else>
          <h2 class="capitalize">{{item.title}}</h2>
        </span>

      </li>
    </ul>
  </q-page>
</template>

<style scoped>
li {
  list-style: none;
}
.capitalize {
  text-transform: capitalize;
  cursor: pointer;
}
.capitalize:hover {
  text-decoration: underline;
}
h2.capitalize {
  cursor: unset;
}
h2.capitalize:hover {
  text-decoration: none;
}

</style>
