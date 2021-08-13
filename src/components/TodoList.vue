<template>
  <div class="hello">
    <form @submit.prevent="createNewTodo">
      <input
        v-model="todoText"
        type="text"
        placeholder="New Todo"
        name="newTodo"
      />
    </form>
    <!--  -->
    <div>
      <button @click="finishAllTodos">Finish All</button>
      <button @click="clearList">Delete All</button>
    </div>
    <!--  -->
    <ul id="todos-list">
      <li v-for="(todo, $index) in todosArray" :key="$index">
        <label :class="{ 'todo-done': todo.done }">
          <input type="checkbox" v-model="todo.done" />
          {{ todo.text }}
        </label>
        <button @click="deleteTodo($index)">X</button>
      </li>
    </ul>
  </div>
</template>

<script>
// {text: "Aprender Vue.js", done: false}
// :class="{done: true}"
// 0, 1, 2... index = 2
// index != 2
export default {
  name: "TodoList",
  data: () => ({
    todoText: "",
    todosArray: [
      { text: "Aprender Vue.js", done: false },
      { text: "Profit", done: false },
    ],
  }),
  methods: {
    createNewTodo() {
      this.todosArray.push({
        text: this.todoText,
        done: false,
      });
      this.todoText = "";
    },
    deleteTodo(removeIndex) {
      const newTodosArray = this.todosArray.filter((_, index) => {
        return removeIndex !== index;
      });

      this.todosArray = newTodosArray;
    },
    finishAllTodos() {
      this.todosArray.map((item) => {
        item.done = true;
        return item;
      });
    },
    clearList() {
      this.todosArray = [];
    },
  },
};
</script>

<style scoped lang="scss">
#todos-list {
  padding: 0;
  margin: 20px auto;
  display: table;
  width: auto;
  list-style: none;
  list-style-type: none;

  li {
    text-align: left;
  }

  label {
    width: 100%;
    max-width: 250px;
    user-select: none;
    text-align: left;
  }
  label,
  button {
    display: inline;
  }

  .todo-done {
    text-decoration: line-through;
  }
}
</style>
