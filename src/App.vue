<template>
  <div :class="$style.container">
    <div :class="$style['widget-wrapper']"><widget /></div>
  </div>
</template>

<script>
import Widget from "./components/Widget.vue";
export default {
  components: { Widget },
};
</script>

<style module lang="scss">
.container {
  width: 500px;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  margin: 0 auto;
  .widget-wrapper {
    width: 100%;
    height: 500px;
    border: 2px solid teal;
  }
  @media (max-width: 500px) {
    width: 100%;
  }
}
</style>