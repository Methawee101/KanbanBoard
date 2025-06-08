<template>
  <div class="container">
    <form @submit.prevent="handleLogin()">
      <h2>Login</h2>
      <div class="input-group">
        <label>email</label>
        <input type="email" require v-model="email" />
      </div>
      <div class="input-group">
        <label>password</label>
        <input type="password" require v-model="password" />
      </div>
      <button type="submit">Login</button>
    </form>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";
import { useRouter } from "vue-router";

export default defineComponent({
  name: "LoginView",
  setup() {
    const email = ref("");
    const password = ref("");

    const router = useRouter();

    const handleLogin = () => {
      const stored = localStorage.getItem("users");
      const users = stored ? JSON.parse(stored) : [];

      const userStoraged = users.find(
        (u: { email: string; password: string }) =>
          u.email.toLowerCase() === email.value.toLowerCase() ||
          u.password === password.value
      );
      if (userStoraged) {
        alert("Login Sucessfull");
        setTimeout(() => {
          router.push("/board");
        }, 1000);
        return;
      }

      email.value = "";
      password.value = "";
    };
    return {
      email,
      password,
      handleLogin,
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
button :hover {
  background-color: #d26161;
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
