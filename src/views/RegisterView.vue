<template>
  <div class="container">
    <form @submit.prevent="handleRegister()">
      <h2>Register</h2>
      <div class="input-group">
        <label>name</label>
        <input type="text" require v-model="name" />
      </div>
      <div class="input-group">
        <label>email</label>
        <input type="email" require v-model="email" />
      </div>
      <div class="input-group">
        <label>password</label>
        <input type="password" require v-model="password" />
      </div>
      <div class="input-group">
        <label>Confirm Password</label>
        <input type="password" require v-model="confirmPassword" />
      </div>
      <button type="submit">Register</button>
    </form>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";
import { useRouter } from "vue-router";

interface User {
  id: string;
  name: string;
  email: string;
  password: string;
}
export default defineComponent({
  name: "RegisterView",
  setup() {
    const name = ref("");
    const email = ref("");
    const password = ref("");
    const confirmPassword = ref("");

    const router = useRouter();

    const generateId = (): string => {
      return Date.now().toString();
    };
    const handleRegister = () => {
      if (password.value !== confirmPassword.value) {
        alert("Passwords do not match");
        return;
      }

      const stored = localStorage.getItem("users");
      const users: User[] = stored ? JSON.parse(stored) : [];

      const exists = users.find(
        (u) => u.email.toLowerCase() === email.value.toLowerCase()
      );

      if (exists) {
        alert("Email already registered.");
        return;
      }

      const newUser: User = {
        id: generateId(),
        name: name.value,
        email: email.value,
        password: password.value,
      };

      users.push(newUser);
      localStorage.setItem("users", JSON.stringify(users));

      alert("Register successful! You can now login.");

      name.value = "";
      email.value = "";
      password.value = "";
      confirmPassword.value = "";

      setTimeout(() => {
        router.push("/login");
      }, 2000);
      console.log(users);
    };

    return {
      name,
      email,
      password,
      confirmPassword,
      handleRegister,
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
  background-color: #d9d9d9;
}
form {
  display: flex;
  flex-direction: column;
  gap: 10px;
  background-color: white;
  color: black;
  border-radius: 20px;
  width: 50%;
  height: 75%;
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
  margin-top: 3%;
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
  margin-top: 25px;
  gap: 3px;
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
