<template>
  <div>
    <Hero />
    <div class="container">
      <ShowMovies :movies="movies" />
      <div class="btn">
        <button class="load" @click="handleLoad">Load More</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  // async asyncData({ $axios, $config }) {
  //   const api = `https://api.themoviedb.org/3/movie/upcoming?api_key=${$config.apiKey}&language=en-US&page=1`
  //   const movies = await $axios.$get(api)
  //   return { movies }
  // },
  data() {
    return {
      page: 1,
      movies: [],
      upcoming: `https://api.themoviedb.org/3/movie/upcoming?api_key=${this.$config.apiKey}&language=en-US&page=${this.page}`,
    }
  },
  head: {
    title: 'Upcoming Movies',
  },
  mounted() {
    this.getMovies()
  },
  methods: {
    async getMovies() {
      const movies = await this.$axios.$get(this.upcoming)
      this.movies.push(...movies.results)
    },
    handleLoad() {
      this.page++
      return this.getMovies()
    },
  },
}
</script>

<style lang="scss" scoped>
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
