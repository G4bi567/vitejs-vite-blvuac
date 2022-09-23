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

function isAvailable(str) {
  return str.match("^[a-zA-Z0-9]+$");
}

const newTodo = reactive({
  title: '',
  done: false,
  id: null,
});

var able = false

const addNewTodo = () => {
  if (isAvailable(newTodo.title)){
    maxId++;
    todos.push({ ...newTodo, id: maxId });
    newTodo.title = '';
  }else{
    able = true;
    alert('10 ${able}')
  }
};


const handleDeleteItem = (id) => {
  const index = todos.findIndex(todo => (todo.id)=id);
  todos.splice(index,1);
}

const debug = ref(false)

</script>

<template>
  <pre v-if="debug">{{ todos }}</pre>
  <form :class="{ shake: able }" class="todo-form">
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

<style scoped>
  .shake {
  animation: shake 0.82s cubic-bezier(0.36, 0.07, 0.19, 0.97) both;
  transform: translate3d(0, 0, 0);
}

@keyframes shake {
  10%,
  90% {
    transform: translate3d(-1px, 0, 0);
  }

  20%,
  80% {
    transform: translate3d(2px, 0, 0);
  }

  30%,
  50%,
  70% {
    transform: translate3d(-4px, 0, 0);
  }

  40%,
  60% {
    transform: translate3d(4px, 0, 0);
  }
}
</style>
