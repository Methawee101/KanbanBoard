<template>
  <div class="container">
    <div class="button-group">
      <button @click="handleButtonRegister()">Register</button>
      <button @click="handleButtonLogin()">Login</button>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import { useRouter } from "vue-router";

export default defineComponent({
  setup() {
    const router = useRouter();

    const handleButtonLogin = (): void => {
      setTimeout(() => {
        router.push("/login");
      }, 2000);
    };

    const handleButtonRegister = (): void => {
      setTimeout(() => {
        router.push("/register");
      }, 2000);
    };

    return {
      handleButtonLogin,
      handleButtonRegister,
    };
  },
});
</script>

<style scoped>
.container {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #d9d9d9;
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
  cursor: pointer;
}
button :hover {
  background-color: #d26161;
}
</style>
