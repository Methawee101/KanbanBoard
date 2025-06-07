<template>
  <div class="container">
    <div class="button-group">
      <button>Register</button>
      <button>Login</button>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  components: {},
});
</script>

<style scoped>
.container {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.button-group {
  display: flex;
  flex-direction: column;
  gap: 30px;
  align-items: center;
}

button {
  background-color: #ff9797;
  border: none;
  width: 350px;
  height: 70px;
  border-radius: 25px;
  font-size: 26px;
  color: white;
}
</style>
