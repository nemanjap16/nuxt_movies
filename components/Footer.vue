<template>
  <footer class="footer">
    <h4>
      &copy; Copyright 2021 -
      {{ new Date().toLocaleString('en-GB', { year: 'numeric' }) }} | Nemanja
      Pantelic
    </h4>
  </footer>
</template>

<script>
export default {}
</script>

<style lang="scss" scoped>
.footer {
  width: 100%;
  min-height: 80px;
  background-color: #0e101a;
  color: rgb(133, 189, 253);
  display: flex;
  justify-content: center;
  align-items: center;

  h4 {
    font-weight: normal;

    &:hover {
      color: #fff;
    }
  }
}
</style>
