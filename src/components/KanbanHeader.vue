<template>
  <div class="container">
    <h1>Kanban Board</h1>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "KanbanHeader",
  setup() {
    return {};
  },
});
</script>

<style scoped>
.container {
  width: 100%;
  height: 80px;
  background-color: #d26161;
  font-weight: bold;
  top: 0;
  left: 0;
  right: 0;
  position: fixed;
  z-index: 1000;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
