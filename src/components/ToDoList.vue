<template>
  <div class="pt-3">
    <transition-group name="fade">
      <v-card
        class="mx-auto pa-3 ma-2 text-center"
        max-width="400"
        v-for="ToDo in ToDos"
        :key="ToDo.id"
      >
        <v-row>
          <v-col cols="8">
            <v-list-item-title class="headline mb-1">{{ ToDo.name }}</v-list-item-title>
            <v-list-item-title class="headline mb-1">{{ ToDo.bio }}</v-list-item-title>
            <v-list-item-title class="headline mb-1">{{ ToDo.location }}</v-list-item-title>
          </v-col>
        </v-row>
      </v-card>
    </transition-group>
  </div>
</template>
<script>
import { db } from "../firebase/db";
export default {
  data() {
    return {
      ToDos: [],
      newItem: ""
    };
  },
  methods: {
    deleteToDo(id) {
      db.collection("ToDos")
        .doc(id)
     
    },
    async addItem() {
      if (this.newItem) {
        await db.collection("ToDos").add({ name: this.newItem });
        await db.collection("ToDos").add({ bio: this.newItem });
           await db.collection("ToDos").add({ location: this.newItem });

        this.newItem = "";
      }
    }
  },
  firestore: {
    ToDos: db.collection("ToDos")
  }
};
</script>
<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to  {
  opacity: 0;
}
</style>
