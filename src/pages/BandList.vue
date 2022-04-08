<script setup>
import { RouterLink } from "vue-router";
import data from "app/newData";
</script>

<template>
  <h1>Band List</h1>

  <ul>
    <li v-for="band in data" :key="band.bandId">
      <div class="q-pa-md">
        <div class="row">
          <div class="col">
            <h2 class="title">
              <RouterLink :to="`/band/${band.bandId}`">{{ band.band }}</RouterLink>
            </h2>
          </div>
        </div>

        <div class="row">
          <div class="col">
            <q-img :src="require(`../assets/${band.image}`)" alt="" />
          </div>
          <div class="col info">
            <p>
              {{band.info.text}} - {{band.info.attribution}}
            </p>
            <q-btn color="primary" label="On to the tabs" :to="`/band/${band.bandId}`"/>
          </div>
        </div>
      </div>
    </li>
  </ul>
</template>

<style>
ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
}

.q-pa-md {
  padding: 0;
}

.col.info {
  padding: 0 25px;
}

.title {
  text-align: center;
}

</style>
