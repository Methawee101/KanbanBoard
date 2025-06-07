<template>
  <div class="container">
    <form>
      <div class="input-group">
        <label>name</label>
        <input type="text" require v-model="username" />
        <label>email</label>
        <input type="email" require v-model="email" />
        <label>password</label>
        <input type="password" require v-model="password" />
      </div>
      <button type="submit">Register</button>
    </form>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  components: {},
  data() {
    return {
      username: "" as string,
      email: "" as string,
      password: "" as string,
    };
  },
});
</script>

<style scoped>
.container {
  display: flex;
  height: 100vh;
  justify-content: center;
  align-items: center;
}
form {
  display: flex;
  flex-direction: column;
  gap: 15px;
  background-color: white;
  color: black;
  border-radius: 20px;
  width: 50%;
  height: 50%;
  justify-content: center;
  align-items: center;
  font-size: 20px;
}
button {
  width: 30%;
  height: 10%;
  border-radius: 20px;
  background-color: #ff9797;
  color: white;
  font-size: 20px;
}
.input-group {
  display: flex;
  flex-direction: column;
  align-items: start;
  width: 200px;
}
input {
  height: 30px;
  width: 100%;
  border-radius: 20px;
  border-color: #d9d9d9;
}
</style>
