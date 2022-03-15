<template>
  <div class="loader">
    <div class="lightblue"></div>
    <div class="darkblue"></div>
  </div>
</template>

<script>
export default {}
</script>

<style lang="scss" scoped>
.loader {
  position: absolute;
  inset: 0;
  min-height: 100vh;
  background-color: #fff;
  display: flex;
  align-items: center;
  justify-content: center;
}

.lightblue,
.darkblue {
  margin: auto;
  position: absolute;
  left: 0;
  top: 0;
  right: 0;
  bottom: 0;
  width: 100px;
  height: 100px;
  border-radius: 50%;
}

.lightblue {
  z-index: 999;
  background-color: rgba(39, 129, 232, 0.3);
  animation: hide1 2s ease infinite;
}

.darkblue {
  background-color: rgba(2, 35, 106, 0.4);
  animation: hide2 2s ease infinite;
}

@keyframes hide1 {
  0% {
    transform: scale(1);
  }
  50% {
    transform: scale(0);
  }
  100% {
    transform: scale(1);
  }
}

@keyframes hide2 {
  0% {
    transform: scale(0);
  }
  50% {
    transform: scale(1);
  }
  100% {
    transform: scale(0);
  }
}
</style>
