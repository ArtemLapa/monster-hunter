<template>
  <div id="app" class="app">
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
@import url("https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700&display=swap");
$style: "app";
.#{$style} {
  font-family: "Roboto", sans-serif;
  &__title {
    text-align: center;
    margin-bottom: 40px;
  }
}
</style>
