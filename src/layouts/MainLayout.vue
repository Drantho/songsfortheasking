<template>
  <q-layout view="lHh Lpr lFf">
    <q-header>

    <q-toolbar class="bg-primary text-white q-my-md ">
      <q-btn flat round dense icon="menu" class="q-mr-sm" @click="toggleLeftDrawer"/>
      <q-separator dark vertical inset />
      <q-btn stretch flat label="Home" to="/" />

      <q-space />

      <q-btn stretch flat label="Song List" to="/songlist" />
      <q-separator dark vertical />
      <q-btn-dropdown stretch flat label="Band List">
        <q-list>
          <q-item clickable v-close-popup tabindex="0" to="/bandlist">
            <q-item-section>
              <q-item-label>Band List</q-item-label>
            </q-item-section>
          </q-item>
          <q-item v-for="n in data" :key="`x.${n}`" clickable v-close-popup tabindex="0" :to="`/band/${n.bandId}`">
            <q-item-section>
              <q-item-label>{{n.band}}</q-item-label>
            </q-item-section>
          </q-item>
        </q-list>
      </q-btn-dropdown>
      <q-separator dark vertical />
      <q-btn stretch flat label="About" />
      <q-separator dark vertical />
      <q-btn stretch flat label="News" />
    </q-toolbar>

    </q-header>
    <Breadcrumb :songId="songId" :albumId="albumId" :bandId="bandId"/>
    <q-drawer
      v-model="leftDrawerOpen"
      bordered
    >
      <q-list>
        <q-item-label
          header
        >

        </q-item-label>
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script setup>
import { ref } from 'vue'
import EssentialLink from 'components/EssentialLink.vue'
import Breadcrumb from 'src/components/Breadcrumb.vue'
import data from '../../newData';
import { RouterLink, useRoute } from 'vue-router';

const leftDrawerOpen = ref(false)

const toggleLeftDrawer = () => {
  leftDrawerOpen.value = !leftDrawerOpen.value
}

const route = useRoute();

const bandId = route.params.bandId;
const albumId = route.params.albumId;
const songId = route.params.songId;


</script>

<style scoped>
.q-page-container {
  max-width: 1200px;
  margin: 0 auto;
}
</style>
