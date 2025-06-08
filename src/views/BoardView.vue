<template>
  <div class="container">
    <div>
      <h1>Task</h1>
    </div>
    <div class="card">
      <CardBoard
        v-for="card in cards"
        :key="card.id"
        :id="card.id"
        :title="card.title"
        :content="card.content"
        @delete="handleDeleteCard"
      />
    </div>
  </div>
  <div>
    <p @click="openModal()">+</p>
    <Modal v-if="isShowModal" @close="closeModal()" @add="addItem" />
  </div>
</template>

<script lang="ts">
import Modal from "@/components/ModalCard.vue";
import CardBoard from "@/components/CardBoard.vue";
import { defineComponent, ref, onMounted } from "vue";

interface Card {
  id: string;
  title: string;
  content: string;
}

export default defineComponent({
  name: "BoardView",
  components: { Modal, CardBoard },
  setup() {
    const isShowModal = ref<true | false>(false);
    const cards = ref<Card[]>([]);

    onMounted(() => {
      const stored = localStorage.getItem("cards");
      if (stored) {
        cards.value = JSON.parse(stored) as Card[];
      }
    });

    const closeModal = () => {
      isShowModal.value = false;
    };

    const openModal = () => {
      isShowModal.value = true;
    };

    const addItem = (card: Card) => {
      cards.value.push(card);
      localStorage.setItem("cards", JSON.stringify(cards.value));
    };

    const handleDelete = (id: string) => {
      cards.value = cards.value.filter((c: Card) => c.id !== id);
      localStorage.setItem("cards", JSON.stringify(cards.value));
    };

    return {
      addItem,
      openModal,
      closeModal,
      isShowModal,
      handleDelete,
    };
  },
});
</script>

<style scoped>
.container {
  display: flex;
  justify-content: space-around;
  color: black;
  font-weight: bold;
  margin-top: 15px;
}
p {
  position: absolute;
  background-color: #fdb1b1;
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
  background-color: #d26161;
}
</style>
