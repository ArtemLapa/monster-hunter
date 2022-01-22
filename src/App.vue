<template>
  <div id="app">
    <h1 class="app__title">Monster Hunter Game</h1>
    <MonsterMain />
  </div>
</template>

<script>
import MonsterMain from "./components/MonsterMain.vue";

export default {
  name: "App",
  components: {
    MonsterMain,
  },
};
</script>

<style lang="scss">
$style: "app";
.#{$style} {
  &__title {
    font-family: "Helvetica Neue";
    text-align: center;
  }
}
</style>
