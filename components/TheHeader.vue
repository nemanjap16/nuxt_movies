<template>
  <header class="header">
    <nav class="main_nav container">
      <nuxt-link :to="{ name: 'index' }">
        <div class="main_nav_logo">TMDB</div>
      </nuxt-link>

      <div class="main_nav_links">
        <NuxtLink class="main_nav_link" :to="{ name: 'index' }"
          >Upcoming Movies</NuxtLink
        >
        <NuxtLink class="main_nav_link" :to="{ name: 'movies' }"
          >Now Playing Movies</NuxtLink
        >
      </div>
    </nav>
  </header>
</template>

<script>
export default {}
</script>

<style lang="scss" scoped>
.header {
  position: fixed;
  top: 0;
  height: 70px;
  width: 100%;
  background: hsl(0 0% 0% / 0.75);
  z-index: 1;
}

@supports (-webkit-backdrop-filter: saturate(180%) blur(20px)) or
  (backdrop-filter: saturate(180%) blur(20px)) {
  .header {
    -webkit-backdrop-filter: saturate(180%) blur(20px);
    backdrop-filter: saturate(180%) blur(20px);
    background: hsl(0 0% 100% / 0.15);
  }
}

.main_nav {
  height: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;

  &_logo {
    font-size: 22px;
    font-weight: 600;
    font-weight: 500;
    letter-spacing: 1.5px;
    width: auto;
    color: #fff;
  }

  &_link {
    margin-right: 25px;
    color: rgb(176, 174, 179);
  }

  &_link:last-child {
    margin-right: 0;
  }
}

.nuxt-link-exact-active {
  color: #fff;
}
</style>
