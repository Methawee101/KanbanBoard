<template>
  <v-card class="card">
    <v-card-text class="texttitle"> ppp </v-card-text>
    <div>
      <p>X</p>
    </div>
    <v-card-text class="content">
      Lorem ipsum dolor sit amet consectetur adipisicing elit. Molestias eaque
      distinctio voluptatem labore voluptatibus! Explicabo consequatur vel,
      assumenda exercitationem quibusdam alias repellat id, aspernatur eius ad
      nihil qui veniam cumque!
    </v-card-text>
  </v-card>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "CardBoard",
  data() {
    return {
      title: "PT" as string,
      content: "" as string,
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
  align-items: center;
  justify-content: center;
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
}
.content {
  color: rgb(99 99 99);
  text-align: center;
  font-weight: 600;
}
p {
  position: absolute;
  background-color: #fdb1b1;
  color: black;
  border-radius: 20px;
  width: 30px;
  height: 30px;
  top: 0;
  right: 10px;
  justify-content: center;
  align-content: center;
  cursor: pointer;
}
p:hover {
  background-color: red;
}
</style>
