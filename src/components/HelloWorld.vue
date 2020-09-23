<template>
  <div>
    <img alt="Vue logo" src="../assets/m5.png" />
    <b-container fluid class="bv-example-row mb-4 mt-2">
      <input type="text" v-model="textSearch" />
      <button @click="searchData()">Serch</button>
    </b-container>
    <template v-if="this.t != ''">
      <b-container fluid class="bv-example-row">
        <b-row align-h="around mr-4 ml-4">
          <b-card
            v-for="list in playlist"
            :key="list.id"
            :title="list.title"
            :img-src="'http://image.tmdb.org/t/p/w600_and_h900_bestv2' + list.poster_path "
            img-top
            tag="article"
            style="max-width: 20rem;"
            class="mb-4"
          >
            <b-button :href="'https://www.themoviedb.org/movie/' + list.id " variant="primary">More</b-button>
          </b-card>
        </b-row>
      </b-container>
    </template>
    <!-- {{ playlist }}-->
  </div>
</template>
<script>
import axios from "axios";
export default {
  data() {
    return {
      playlist: null,
      textSearch: "",
      t: this.textSearch,
    };
  },
  methods: {
    searchData() {
      axios
        .get(
          "https://api.themoviedb.org/3/search/movie?query=" +
            this.textSearch +
            "&api_key=feb6f0eeaa0a72662967d77079850353"
        )
        .then((Response) => {
          this.playlist = Response.data.results;
        })
        .catch((err) => {
          console.log(err);
          this.err = true;
        });
    },
  },
};
</script>
<style>
body {
  background-image: url("../assets/bg.jpg");
}
</style>