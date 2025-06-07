<template>
  <KanbanHeader />
  <!-- <HomeView /> -->
  <RegisterView />
</template>

<script lang="ts">
import { defineComponent } from "vue";
import KanbanHeader from "./components/KanbanHeader.vue";
// import HomeView from "./views/HomeView.vue";
import RegisterView from "./views/RegisterView.vue";

export default defineComponent({
  name: "App",
  components: {
    KanbanHeader,
    // HomeView,
    RegisterView,
  },
});
</script>

<style>
#app {
  padding-top: 80px;
  height: 100vh;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: White;
  background-color: #d9d9d9;
}
</style>
