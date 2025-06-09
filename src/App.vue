<template>
  <KanbanHeader />
  <router-view />
</template>

<script lang="ts">
import { defineComponent } from "vue";
import KanbanHeader from "./components/KanbanHeader.vue";

export default defineComponent({
  name: "App",
  components: {
    KanbanHeader,
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
}
</style>
