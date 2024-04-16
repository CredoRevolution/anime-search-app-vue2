<template>
  <div id="app">
    <header>
      <h1>The <strong>Anime</strong>DataBase</h1>
      <form class="search-box" @submit.prevent="getAnime">
        <input
          type="search"
          placeholder="Search for an anime"
          class="search-field"
          required
          v-model="search"
        />
      </form>
    </header>
    <main>
      <div class="cards">
        <Card v-for="anime in animeList" :key="anime.mal_id" :anime="anime" />
      </div>
    </main>
  </div>
</template>

<script>
import { reactive, ref } from 'vue'
import Card from './components/Card.vue'

const search = ref('')
const animeList = ref([])

export default {
  name: 'App',
  components: {
    Card,
  },
  data() {
    return {
      search,
      animeList,
    }
  },
  methods: {
    getAnime() {
      fetch(`https://api.jikan.moe/v4/anime?q=${this.search}&sfw`)
        .then((response) => response.json())
        .then((data) => {
          animeList.value = data.data
          console.log(animeList)
        })
        .catch((error) => console.log(error))
    },
  },
}
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;

  font-family: 'Fira sans', sans-serif;
}

a {
  text-decoration: none;
}

header {
  padding-top: 50px;
  padding-bottom: 50px;
  h1 {
    color: #888;
    font-size: 42px;
    font-weight: 400;
    text-align: center;
    text-transform: uppercase;
    margin-bottom: 30px;
    strong {
      color: #313131;
    }
  }
  .search-box {
    display: flex;
    justify-content: center;
    padding-left: 30px;
    padding-right: 30px;
    .search-field {
      appearance: none;
      border: none;
      outline: none;
      background: none;
      background-color: #f3f3f3;
      padding: 10px 15px;
      border-radius: 8px;
      box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.1);
      display: block;
      width: 100%;
      max-width: 600px;

      columns: #313131;
      font-size: 20px;

      transition: 0.4s;

      &::placeholder {
        color: #aaa;
      }

      &:focus,
      &:valid {
        box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
        background-color: #313131;
        color: #fff;
      }
    }
  }
}

main {
  padding-left: 30px;
  padding-right: 30px;
  max-width: 1200px;
  margin: 0 auto;
  .cards {
    display: flex;
    flex-wrap: wrap;
    margin: 0 -8px;
  }
}
</style>
