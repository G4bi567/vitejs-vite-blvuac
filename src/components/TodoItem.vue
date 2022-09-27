<script setup>
import { ref, reactive } from 'vue';

const props = defineProps({
  todo: Object,
});

const mode = ref('view');

const enterEditMode = (event) => {
  mode.value = 'edit';
  Editinputfocus()
};

const enterViewMode = (event) => {
  mode.value = 'view';

};

const Editinputfocus = (event) => {
  alert("bonjour")
  this.$refs.editinput.focus()
  alert("bo")
}

</script>

<template>
  <span class="todo-collection__item__title" :class="{ strike:!todo.done }" v-show="mode === 'view'"
    >{{ todo.title }}
  </span>
  <input
    class="input input--todo"
    type="text"
    v-model="todo.title"
    ref="editinput"
    v-show="mode === 'edit'"
  /><button
    class="button button--todo button--edit"
    v-show="mode === 'view'"
    @click="enterEditMode"
  >
    Editer
  </button>
  <button
    class="button button--todo button--save"
    v-show="mode === 'edit'"
    @click="enterViewMode"
  >
    Sauvegarder
  </button>
  <button 
    class="button button--todo button--delete"
    @click="$emit(`deleteItem`, todo.id)"
  >
    Supprimer
  </button>
  <button class="button button--todo" @click="todo.done= !todo.done">{{todo.done ? "Effectué" : "Pas Effectué"}}</button>
</template>

<style scoped></style>
