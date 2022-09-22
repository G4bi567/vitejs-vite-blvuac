<script setup>
import { ref, reactive } from 'vue';
import TodoItem from './TodoItem.vue';

const todos = reactive([
  {
    title: 'pommes',
    done: true,
    id: 1,
  },
  {
    title: 'fraises',
    done: true,
    id: 2,
  },
  {
    title: 'ananas',
    done: true,
    id: 3,
  },
]);

let maxId = 3;

const newTodo = reactive({
  title: '',
  done: false,
  id: null,
});

const addNewTodo = () => {
  maxId++;
  todos.push({ ...newTodo, id: maxId });
  newTodo.title = '';
};

const handleDeleteItem = (id) => {
  const index = todos.findIndex(todo => (todo.id)=id);
  todos.splice(index,1);
}

const debug = ref(true)

</script>

<template>
  <pre v-if="debug">{{ todos }}</pre>
  <form class="todo-form">
    <div class="input-field">
      <input
        v-model="newTodo.title"
        ref="input"
        type="text"
        id="input--add"
        class="input"
        placeholder="Que voulez-vous faire ?"
      />
      <label for="input--add"></label>
    </div>
    <input
      type="submit"
      class="button button--add"
      value="Ajouter"
      @click.prevent="addNewTodo"
    />
  </form>
  <ul class="todo-collection">
    <li v-for="todoItem in todos" class="todo-collection__item">
      <todo-item :todo="todoItem" @deleteItem="handleDeleteItem"></todo-item>
    </li>
  </ul>
</template>

<style scoped></style>
