<template>
  <div class="modal-container">
    <div class="modal">
      <p class="close-button" @click="close">X</p>
      <form @submit.prevent="handleSubmit">
        <div class="input-group">
          <label>Title</label>
          <textarea v-model="title" id=""></textarea>
        </div>
        <div class="input-group">
          <label>content</label>
          <textarea v-model="content"></textarea>
        </div>
        <button type="submit" class="btn-submit">{{ props.buttonText }}</button>
      </form>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, watch, PropType } from "vue";

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

const generateId = (): string => {
  return Date.now().toString();
};

export default defineComponent({
  props: {
    mode: {
      type: String as PropType<"add" | "edit">,
      default: "add",
    },
    buttonText: {
      type: String,
      default: "Add",
    },
    cardData: {
      type: Object as PropType<Partial<Card>>,
      default: () => ({ id: "", title: "", content: "", members: [] }),
    },
  },

  name: "ModalCard",
  emits: ["close", "add", "edit"],
  setup(props, { emit }) {
    const title = ref(props.cardData.title || "");
    const content = ref(props.cardData.content || "");

    watch(
      () => props.cardData,
      (newData) => {
        title.value = newData.title || "";
        content.value = newData.content || "";
      },
      { immediate: true, deep: true }
    );

    const handleSubmit = () => {
      if (!title.value.trim() || !content.value.trim()) {
        alert("Plz add Title and Content");
        return;
      }
      const newCard: Card = {
        id: props.cardData.id || generateId(),
        title: title.value,
        content: content.value,
        members: props.cardData.members || [],
      };
      console.log("Emitting new card:", newCard);

      if (props.mode === "edit") {
        emit("edit", newCard);
      } else {
        emit("add", newCard);
      }

      title.value = "";
      content.value = "";
      emit("close");
    };
    return {
      title,
      content,
      handleSubmit,
      props,
      close: () => emit("close"),
    };
  },
});
</script>

<style scoped>
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
