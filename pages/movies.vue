<template>
  <div>
    <Hero />
    <div class="container">
      <div class="search">
        <input
          v-model="searchInput"
          type="text"
          placeholder="search movies ..."
          @keypress.enter="$fetch"
        />
      </div>
      <ShowMovies v-if="searchInput === ''" :movies="movies" />
      <searched-movie v-else :movies="searched" />
      <div v-show="totalPages >= searchPage" class="btn">
        <button class="load" @click="handleLoad">Load More</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      page: 1,
      searchPage: 1,
      movies: [],
      searched: [],
      searchInput: '',
      query: '',
      totalPages: 1,
    }
  },
  fetchDelay: 1000,
  async fetch() {
    if (this.searchInput === '') {
      this.searched = []
      await this.getMovies()
    } else {
      this.searched = []
      await this.searchMovie(this.searchInput)
    }
  },
  methods: {
    async getMovies() {
      const movies = await this.$axios.$get(
        `https://api.themoviedb.org/3/movie/now_playing?api_key=${this.$config.apiKey}&language=en-US&page=${this.page}`
      )
      this.movies.push(...movies.results)
    },
    async searchMovie(query) {
      const search = await this.$axios.$get(
        `https://api.themoviedb.org/3/search/movie?api_key=${this.$config.apiKey}&language=en-US&query=${query}&page=${this.searchPage}&include_adult=false`
      )
      this.searched.push(...search.results)
      this.totalPages = search.total_pages
    },
    handleLoad() {
      if (this.searchInput === '') {
        this.page++
        return this.getMovies()
      } else {
        this.searchPage++
        this.query = this.searchInput
        this.searchInput = this.query
        return this.searchMovie(this.query)
      }
    },
  },
}
</script>

<style lang="scss" scoped>
input {
  border: none;
  outline: none;
  padding: 12px;
  width: 400px;
}

.search {
  margin-top: 50px;
  display: flex;
  align-items: center;
  justify-content: center;

  input {
    border-radius: 5px;
  }
}

.btn {
  text-align: center;
  width: 100%;
  margin-bottom: 40px;
}

.load {
  padding: 10px 26px;
  font-size: 17px;
  border-radius: 6px;
  color: whitesmoke;
  background-color: cornflowerblue;
  appearance: none;
  outline: none;
  border: none;
  cursor: pointer;
}
</style>
