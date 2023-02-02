<template>
  <div :class="$style.container">
    <div
      :class="$style.logo"
    ></div>
    <span :class="$style.text">Weather Widget</span>
  </div>
</template>

<script>
export default {};
</script>

<style module lang="scss">
.container {
  width: 100%;
  height: 3em;
  display: flex;
  align-items: center;
  justify-content: space-between;
  .logo {
    width: 3em;
    height: 100%;
    background-size: contain;
    background: url('../../public/cloud.svg') no-repeat no-repeat center;
  }
  .text {
    font-size: 1.4em;
  }
}
</style>