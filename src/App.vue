<template>
  <div id="app" class="app">
    <img alt="Studio Ghibli" src="./assets/logo.png" />
    <SearchInput placeholder="Search by title, director, producer, release date or characters." />
    <div class="container">
      <Card 
        v-for="(film, index) in films"
        :key="index" 
        :title="film.title"
        :description="film.description"
        :director="film.director"
        :producer="film.producer"
        :release="film.release"
      />
    </div>
  </div>
</template>

<script>
import SearchInput from "./components/SearchInput.vue";
import Card from "./components/Card.vue";
import axios from "axios";

export default {
  components: { SearchInput, Card },
  data() {
    return {
      films: [],
    };
  },
  mounted() {
    axios.get("https://ghibliapi.herokuapp.com/films")
      .then(res => { 
        this.films = res.data.map(film => {
          return {
            id: film.id,
            title: film.title,
            description: film.description.length > 300 ? film.description.substring(0, 300) + "..." : film.description,
            director: film.director,
            producer: film.producer,
            release: film.release_date,          
          }
        })
      })
      .catch(error => { console.log(error) })
  }
};
</script>

<style lang="scss">
.app {
  font-family: "Dosis", sans-serif;
  background: $bg-color;
  text-align: center;

  & img {
    margin: 1rem auto;
  }
}

.container {
  max-width: 1200px;
  display: flex;
  flex-wrap: wrap;
  margin: .7rem auto 0;
}
</style>
