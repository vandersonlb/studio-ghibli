<template>
  <div id="app" class="app">
    <img alt="Studio Ghibli" src="./assets/logo.png" />
    <input type="search" class="container__input" @input="search = $event.target.value" placeholder="Search by title, director, producer, release date or characters." />
    <div class="container">
      <Card
        v-for="(film, index) in filteredFilms"
        :key="index"
        :title="film.title"
        :description="film.description"
        :director="film.director"
        :producer="film.producer"
        :release="film.release"
        :characters="film.characters"
      />
    </div>
  </div>
</template>

<script>
import Card from "./components/Card.vue";
import axios from "axios";

export default {
  components: { Card },
  data() {
    return {
      films: [],
      filterFilms: [],
      search: "",
    };
  },
  mounted() {
    axios
      .get("https://ghibliapi.herokuapp.com/films")
      .then((res) => {
        let films = res.data;
        axios
          .get("https://ghibliapi.herokuapp.com/people")
          .then((res) => {
            let peoples = res.data;
            this.films = films.map((film) => {
              return {
                title: film.title,
                description: film.description.length > 300 ? `${film.description.substring(0, 300)}...` : film.description,
                director: film.director,
                producer: film.producer,
                release: film.release_date,
                characters: peoples
                  .filter((people) => people.films.includes(film.url))
                  .map((people) => people.name)
                  .join(", "),
              };
            });
          })
          .catch((err) => console.log(err));
      })
      .catch((err) => console.error(err));
  },
  computed: {
    filteredFilms() {
      if(!this.search) return this.films
      let regexp = new RegExp(this.search.trim(), 'i');
      // return this.films.filter(film => regexp.test(Object.values(film).join()))
      return this.films.filter(film => regexp.test(Object.values(`${film.title} ${film.director} ${film.producer} ${film.release} ${film.characters}`).join("").replace(',','')))
    }
  }
};
</script>

<style lang="scss">
.app {
  font-family: "Dosis", sans-serif;
  background: $bg-color;
  text-align: center;
  min-height: 100vh;

  & img {
    margin: 1rem auto;
  }
}

.container {
  width: 80%;
  max-width: 1200px;
  display: flex;
  flex-wrap: wrap;
  margin: 0.7rem auto 0;
}

input {
  display: block;
  margin: 0 auto;
  width: 80%;
  max-width: 800px;
  border: 1px solid lighten($text-color, 20);
  border-radius: 20px;
  padding: 0.5rem 1rem;
  color: $text-color;
  outline: none;
  background-color: transparent;

  &::-webkit-search-cancel-button {
    -webkit-appearance: none;
    background-color: $text-color;
    height: 12px;
    width: 12px;
    border-radius: 50%;
    opacity: .7;
  }

  &::placeholder {
    color: $text-color;
    opacity: 0.5;
  }

  &:focus {
    border-color: darken($text-color, 10);
  }
}
</style>
