<template>
  <div class="container">
    <form>
      <h2>Login</h2>
      <div class="input-group">
        <label>email</label>
        <input type="email" require v-model="email" />
      </div>
      <div class="input-group">
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
      confirmpassword: "" as string,
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
  gap: 20px;
  background-color: white;
  color: black;
  border-radius: 20px;
  width: 40%;
  height: 50%;
  justify-content: center;
  align-items: center;
  font-size: 20px;
}
button {
  width: 25%;
  height: 10%;
  border-radius: 20px;
  background-color: #ff9797;
  color: white;
  font-size: 20px;
  border: none;
  margin-top: 5%;
  cursor: pointer;
}
.input-group {
  display: flex;
  flex-direction: column;
  align-items: start;
  width: 80%;
  margin-top: 10px;
  gap: 5px;
  align-items: center;
}
input {
  background-color: #eee;
  align-items: center;
  border: none;
  padding: 1rem;
  font-size: 1rem;
  width: 90%;
  border-radius: 1rem;
  color: #333333;
  box-shadow: 0 0.4rem #dfd9d9;
  cursor: pointer;
}
input:focus {
  outline-color: lightcoral;
}
label {
  align-self: flex-start;
}
</style>
