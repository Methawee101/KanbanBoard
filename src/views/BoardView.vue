<template>
  <div class="container">
    <div>
      <h1>Task</h1>
    </div>
    <div class="card-container">
      <CardBoard
        v-for="card in cards"
        :key="card.id"
        :id="card.id"
        :title="card.title"
        :content="card.content"
        :mode="'add'"
        @delete="handleDelete"
        @edit="updateCard"
        :cardData="card"
      />
    </div>
  </div>
  <div>
    <p @click="openModal()">+</p>
    <ModalCard v-if="isShowModal" @close="closeModal()" @add="addItem" />
  </div>
</template>

<script lang="ts">
import ModalCard from "@/components/ModalCard.vue";
import CardBoard from "@/components/CardBoard.vue";
import { defineComponent, ref, onMounted } from "vue";

interface Member {
  id: string;
  name: string;
  email: string;
}
interface Card {
  id: string;
  title: string;
  content: string;
  members: Member[];
}

export default defineComponent({
  name: "BoardView",
  components: { ModalCard, CardBoard },
  setup() {
    const isShowModal = ref<true | false>(false);
    const cards = ref<Card[]>([]);

    onMounted(() => {
      const stored = localStorage.getItem("cards");
      console.log("Stored cards from localStorage:", stored);
      if (stored) {
        cards.value = JSON.parse(stored) as Card[];
        console.log("Parsed cards:", cards.value);
      }
    });

    const closeModal = () => {
      isShowModal.value = false;
      console.log("Modal close");
    };

    const openModal = () => {
      isShowModal.value = true;
      console.log("Modal opened");
    };

    const addItem = (card: Card) => {
      console.log("Receivd card:", card);
      cards.value.push(card);
      localStorage.setItem("cards", JSON.stringify(cards.value));
      console.log("update cards:", cards.value);
    };

    const updateCard = (updatedCard: Card) => {
      const index = cards.value.findIndex((c) => c.id === updatedCard.id);
      if (index !== -1) {
        cards.value[index] = updatedCard;
        localStorage.setItem("cards", JSON.stringify(cards.value));
        console.log("Card updated:", cards.value[index]);
      }
    };

    const handleDelete = (id: string) => {
      console.log("Deleting card with id:", id);
      cards.value = cards.value.filter((c: Card) => c.id !== id);
      localStorage.setItem("cards", JSON.stringify(cards.value));
      console.log("Cards after deletion:", cards.value);
    };

    return {
      addItem,
      openModal,
      closeModal,
      isShowModal,
      handleDelete,
      cards,
      updateCard,
    };
  },
});
</script>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  justify-content: start;
  color: black;
  font-weight: bold;
  background-color: #d9d9d9;
  height: 100vh;
}
p {
  position: fixed;
  background-color: #d26161;
  color: black;
  border-radius: 50px;
  width: 70px;
  height: 70px;
  bottom: 0;
  right: 30px;
  justify-content: center;
  align-content: center;
  cursor: pointer;
  font-size: 40px;
}
p:hover {
  background-color: #fdb1b1;
}
.card-container {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap; /* ป้องกันการ์ดตกลงบรรทัดใหม่ */
  gap: 20px; /* ระยะห่างระหว่างการ์ด */
  overflow-x: auto; /* ถ้าการ์ดเยอะ ให้เลื่อนแนวนอน */
  padding: 10px;
  width: 100%;
}
</style>
