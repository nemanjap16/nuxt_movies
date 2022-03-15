<template>
  <div class="banner">
    <h1>TMDB Movies</h1>
    <p>Find movies you like</p>
  </div>
</template>

<script>
export default {}
</script>

<style lang="scss" scoped>
.banner {
  height: 40vh;
  overflow: hidden;
  background: linear-gradient(
      to bottom,
      rgba(5, 2, 49, 0.75),
      rgba(5, 2, 49, 0.9)
    ),
    url('/sonic2.jpg') no-repeat center center;
  background-size: cover;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;

  h1 {
    color: #fff;
    font-size: 3rem;
    font-weight: bold;
    letter-spacing: 3.6px;
    text-shadow: 0 0 10px #000;
  }

  p {
    color: #fff;
    font-size: 1.5rem;
    font-weight: bold;
    letter-spacing: 2.8px;
    text-shadow: 0 0 10px #000;
  }
}
</style>
