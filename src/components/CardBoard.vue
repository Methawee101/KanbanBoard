<template>
  <v-card class="card">
    <div class="texttitle">
      {{ title }}
    </div>
    <div class="btn-group">
      <p @click="openModal" class="user">&#128100;</p>
      <p @click="openModalCard" class="edit">&#128393;</p>
      <p @click="deleteCard" class="delete">X</p>
    </div>
    <div class="content">
      {{ content }}
    </div>
  </v-card>
  <ModalCard
    v-if="isShowModalCard"
    @edit="handleEdit"
    @close="closeModalCard()"
    :mode="'edit'"
    :buttonText="'Edit'"
    :cardData="{ id, title, content, members: [] }"
  />
  <ModalUser v-if="isShowModal" @close="closeModal()" :card-id="id" />
</template>

<script lang="ts">
import { defineComponent, ref, PropType } from "vue";
import ModalUser from "./ModalUser.vue";
import ModalCard from "./ModalCard.vue";

interface Member {
  id: string;
  email: string;
}

interface Card {
  id: string;
  title: string;
  content: string;
  members: Member[];
}

export default defineComponent({
  name: "CardBoard",
  components: { ModalUser, ModalCard },
  props: {
    id: {
      type: String as () => string,
      required: true,
    },
    title: {
      type: String as () => string,
      required: true,
    },
    content: {
      type: String as () => string,
      required: true,
    },
    cardData: {
      type: Object as PropType<Card>,
      required: true,
    },
  },
  emits: ["delete", "edit"],
  setup(props, { emit }) {
    const isShowModal = ref<true | false>(false);
    const isShowModalCard = ref<true | false>(false);
    const cards = ref<Card[]>([]);

    const deleteCard = () => {
      emit("delete", props.id);
    };
    const updateCard = (updatedCard: Card) => {
      const index = cards.value.findIndex((card) => card.id === updatedCard.id);
      if (index !== -1) {
        cards.value[index] = updatedCard;

        localStorage.setItem("cards", JSON.stringify(cards.value));
      }
    };
    const handleEdit = (updatedCard: Card) => {
      emit("edit", updatedCard);
      closeModalCard();
    };

    const closeModal = () => {
      isShowModal.value = false;
    };

    const openModal = () => {
      isShowModal.value = true;
    };
    const closeModalCard = () => {
      isShowModalCard.value = false;
    };

    const openModalCard = () => {
      isShowModalCard.value = true;
    };
    return {
      deleteCard,
      openModal,
      closeModal,
      isShowModal,
      openModalCard,
      closeModalCard,
      isShowModalCard,
      updateCard,
      handleEdit,
    };
  },
});
</script>

<style scoped>
.card {
  width: 300px;
  height: 250px;
  background-color: #fdb1b1;
  border-radius: 10px;
  display: flex;
  flex-direction: column;
  justify-content: start;
  padding: 20px 30px;
  gap: 10px;
  position: relative;
  box-shadow: 2px 2px 20px rgba(0, 0, 0, 0.062);
  margin: 45px;
  cursor: pointer;
}
.texttitle {
  font-size: 1.2em;
  font-weight: 800;
  color: rgb(26, 26, 26);
  margin-top: 50px;
}
.content {
  color: rgb(99 99 99);
  text-align: center;
  font-weight: 600;
}
.btn-group {
  display: flex;
  gap: 20px;
  position: absolute;
  top: 0;
  right: 10px;
}
.user {
  background-color: #fdb1b1;
  color: black;
  border-radius: 50%;
  width: 30px;
  height: 30px;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  font-size: 20px;
  line-height: 30px;
}
.delete {
  /* background-color: #fdb1b1; */
  color: black;
  border-radius: 50%;
  width: 30px;
  height: 30px;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  font-size: 20px;
  line-height: 30px;
}
.edit {
  color: black;
  border-radius: 50%;
  width: 30px;
  height: 30px;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  font-size: 20px;
  line-height: 30px;
}
.delete:hover {
  background-color: red;
}
.user:hover {
  box-shadow: 2px 2px 2px 0.5px;
}
.edit:hover {
  box-shadow: 2px 2px 2px 0.5px;
}
</style>
