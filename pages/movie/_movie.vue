<template>
  <div class="container">
    <p class="back" @click="goToPrev()">&larr; back</p>
    <div
      class="img-fluid"
      :style="{
        background: `url(${poster.image}) no-repeat center center`,
      }"
    >
      <div class="overlay">
        <h1>
          {{ movie.title }}
        </h1>
        <p>- {{ movie.tagline }} -</p>
      </div>
    </div>
    <div class="movie_details">
      <div class="poster_wrapper">
        <img
          class="movie_poster"
          :src="`https://image.tmdb.org/t/p/w1280/${movie.backdrop_path}`"
          :alt="`${movie.title} backdrop`"
        />
      </div>
      <div class="details">
        <h1 class="movie_title">{{ movie.title }}</h1>
        <p v-for="genre in movie.genres" :key="genre.name" class="movie_genre">
          &#8280; {{ genre.name }} &#8280;
        </p>
        <div class="movie_overview">{{ movie.overview }}</div>
        <div class="movie_rating">
          <span class="movie_rating_label">Rating:</span>
          <span class="movie_rating_value">{{ movie.vote_average }}</span>
        </div>
        <div class="movie_release_date">
          <span class="movie_release_date_label">Release Date:</span>
          <span class="movie_release_date_value">
            {{
              new Date(movie.release_date).toLocaleString('en-GB', {
                day: 'numeric',
                month: 'long',
                year: 'numeric',
              })
            }}</span
          >
        </div>
        <div class="movie_budget">
          <span class="movie_budget_label">Budget:</span>
          <span class="movie_budget_value">{{ movie.budget }}$</span>
        </div>
        <div class="movie_budget">
          <span class="movie_runtime_label">Runtime:</span>
          <span class="movie_runtime_value">{{ movie.runtime }} min</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  async asyncData({ $config, params, $axios }) {
    const movie = await $axios.$get(
      `https://api.themoviedb.org/3/movie/${params.movie}?api_key=${$config.apiKey}&language=en-US`
    )
    return { movie }
  },
  data() {
    return {
      movie: {},
    }
  },
  head() {
    return {
      title: this.movie.title,
    }
  },
  computed: {
    poster() {
      return {
        image: `https://image.tmdb.org/t/p/original/${this.movie.poster_path}`,
      }
    },
  },
  methods: {
    goToPrev() {
      this.$router.back()
    },
  },
}
</script>

<style lang="scss" scoped>
.movie_details {
  padding: 50px 0;
  width: 100%;
  height: 100%;
  display: flex;
  align-items: flex-start;
  flex-flow: wrap;
}

.poster_wrapper {
  min-width: 450px;
  width: 55%;
  margin-bottom: 50px;
  border-radius: 20px;
  overflow: hidden;
}

.details {
  color: #fff;
  min-width: 450px;
  width: 45%;
  padding: 0 0 0 50px;
  font-weight: normal;

  .movie_title {
    letter-spacing: 2px;
    font-size: 24px;
    font-weight: 500;
  }

  .movie_tagline {
    font-size: 18px;
    letter-spacing: 2.6px;
    font-weight: 400;
    margin: 15px 0;
  }

  .movie_overview {
    margin: 15px 0;
    line-height: 1.6;
    font-weight: 300;
  }

  .movie_rating_label,
  .movie_release_date_label,
  .movie_budget_label,
  .movie_runtime_label {
    color: aqua;
    margin-right: 4px;
  }
}

.img-fluid {
  position: relative;
  max-width: 100%;
  height: 300px;
  border-radius: 20px;
  overflow: hidden;
  background: linear-gradient(
    to bottom,
    rgba(0, 0, 0, 0.5),
    rgba(0, 0, 0, 0.5)
  );
  background-size: cover;
  margin: 40px 0 0 0;

  .overlay {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.35);
    backdrop-filter: saturate(180%) blur(6px);
    border-radius: 20px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    color: whitesmoke;
    font-size: 22px;
    font-weight: 500;
    letter-spacing: 4px;

    h1 {
      font-weight: 400;
    }

    p {
      letter-spacing: 1.6px;
      font-weight: 300;
      font-style: italic;
    }
  }
}

.movie_genre {
  display: inline-block;
  margin-top: 10px;
  color: orange;
}

.back {
  margin-top: 100px;
  color: orange;
  font-size: 20px;
  cursor: pointer;
}
</style>

