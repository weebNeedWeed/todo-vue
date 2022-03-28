<script setup>
import { ref } from "vue";
import { v4 as uuidv4 } from "uuid";

const textInput = ref("");
const todoList = ref([]);

const onUserSubmit = () => {
  const newTodo = {
    id: uuidv4(),
    name: textInput.value,
  };

  todoList.value.push(newTodo);
};

const onDelete = (id) => {
  todoList.value = [...todoList.value].filter((elm) => elm.id !== id);
};
</script>

<template>
  <div class="container">
    <form class="form" @submit.prevent="onUserSubmit">
      <input type="text" class="form__input" v-model="textInput" />
      <button class="form__submit">
        <i class="material-icons">add</i>
      </button>
    </form>

    <ul class="list">
      <li v-for="(todo, index) in todoList" :key="todo.id" class="list__item">
        <p class="list__text">{{ index + 1 }}. {{ todo.name }}</p>

        <button class="list__delete" @click="onDelete(todo.id)">
          <i class="material-icons">delete</i>
        </button>
      </li>
    </ul>
  </div>
</template>

<style lang="scss">
body {
  font-family: "Pacifico", cursive;
}

.container {
  padding: 200px 10px 0px;
  margin: 0 auto;
  box-sizing: border-box;
  width: 100%;
  max-width: 800px;
}

.form {
  width: 100%;
  display: flex;
  justify-content: space-between;
  border: 2px solid rgba(0, 0, 0, 0.4);
  border-radius: 6px;
  box-sizing: border-box;
  padding: 10px;
  &__input {
    flex-basis: 93%;
    border: none;
    border-radius: inherit;
    font-size: 30px;

    &:focus {
      outline: none;
    }
  }

  &__submit {
    flex-basis: 5%;
    border: none;
    background-color: transparent;
    display: flex;
    align-items: center;
    transition: all 0.3s;
    justify-content: center;
    border-radius: 2px;

    &:hover {
      background-color: rgba(0, 0, 0, 0.05);
    }

    &:active {
      background-color: rgba(0, 0, 0, 0.1);
    }
  }
}

.list {
  font-size: 20px;
  list-style-type: none;

  &__item {
    display: flex;
    justify-content: flex-start;
    align-items: center;
  }

  &__delete {
    border: none;
    background-color: transparent;
  }
}
</style>