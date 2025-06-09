<template>
  <div class="modal-container">
    <div class="modal">
      <p class="close-button" @click="close">X</p>
      <form @submit.prevent="handleSubmit">
        <div class="input-group">
          <label>email</label>
          <textarea v-model="email"></textarea>
        </div>
        <button type="submit" class="btn-submit">Add</button>
      </form>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";

interface Member {
  id: string;
  email: string;
}

interface User {
  id: string;
  name: string;
  email: string;
  members: Member[];
}

export default defineComponent({
  name: "ModalUser",
  emits: ["close"],
  props: {
    cardId: { type: String, required: true },
  },
  setup(props, { emit }) {
    const email = ref("");

    const handleSubmit = () => {
      if (!email.value.trim()) {
        alert("Plz enter Email");
        return;
      }
      const storedUsers = localStorage.getItem("users");
      const users: User[] = storedUsers ? JSON.parse(storedUsers) : [];

      const storedCards = localStorage.getItem("cards");
      const cards = storedCards ? JSON.parse(storedCards) : [];

      const cardIndex = cards.findIndex(
        (card: any) => card.id === props.cardId
      );
      if (cardIndex === -1) {
        alert("Card not found.");
        return;
      }

      const Userstored = users.find(
        (user) => user.email.toLowerCase() === email.value.trim().toLowerCase()
      );
      if (!Userstored) {
        alert("User not found.");
        return;
      }

      const card = cards[cardIndex];
      if (!Array.isArray(card.members)) {
        card.members = [];
      }

      const alreadyInCard = card.members.some(
        (member: Member) => member.email === Userstored.email
      );

      if (alreadyInCard) {
        alert("Member is already in this card.");
        return;
      }

      card.members.push({
        id: Userstored.id,
        email: Userstored.email,
      });

      localStorage.setItem("cards", JSON.stringify(cards));

      alert("Member added!");
      email.value = "";
      emit("close");
    };
    return {
      handleSubmit,
      email,
      close: () => emit("close"),
    };
  },
});
</script>

<style>
.modal-container {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100vh;
  background-color: rgba(0, 0, 0, 0.4);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 99;
}
.modal {
  background-color: #ffffff;
  border-radius: 16px;
  padding: 32px;
  width: 90%;
  max-width: 500px;
  position: relative;
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.15);
}

form {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.input-group {
  display: flex;
  flex-direction: column;
}

label {
  font-weight: bold;
  margin-bottom: 8px;
  color: #333;
}

textarea {
  padding: 12px;
  font-size: 16px;
  border: 1px solid #ddd;
  border-radius: 10px;
  resize: none;
  font-family: inherit;
  background-color: #f9f9f9;
}

textarea:focus {
  outline: none;
  border-color: #ff9797;
  background-color: #fff;
}

.btn-submit {
  padding: 12px;
  border: none;
  border-radius: 10px;
  background-color: #ff9797;
  color: white;
  font-size: 18px;
  cursor: pointer;
  transition: background-color 0.2s ease;
}

.btn-submit:hover {
  background-color: #d26161;
}

.close-button {
  position: absolute;
  top: 0px;
  right: 16px;
  border: none;
  background-color: #fdb1b1;
  border-radius: 20px;
  width: 30px;
  height: 30px;
  font-size: 20px;
  color: black;
  cursor: pointer;
  font-weight: bold;
  justify-content: center;
  align-content: center;
}

.close-button:hover {
  background-color: red;
}
</style>
