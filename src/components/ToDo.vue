<template>
  <div class="ToDo">
    <h1>TO-DO LIST</h1>
    <div class="holder">
      <form @submit.prevent="addItem">
        <input
          type="text"
          placeholder="Add An Item"
          v-model="todo"
          name="todo"
          id="todo"
        />
      </form>
      <ul>
        <transition-group
          name="list1"
          enter-active-class="animated bounceInUp"
          leave-active-class="animated bounceOutDown"
        >
          <li v-for="(data, index) in todos" :key="index">
            <input
              type="checkbox"
              id="checkbox"
              v-model="data.done"
              @change="reorderItems(data)"
            />
            <span :class="{ done: data.done }"> {{ data.todo }}</span>
            <button @click="removeTodo(data)" type="button" name="button">
              Remove
            </button>
          </li>
        </transition-group>
      </ul>
      <p>These are the to do list.</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "ToDo",
  data() {
    return {
      todo: "",
      todos: [
        { todo: "1", done: false },
        { todo: "2", done: false },
        { todo: "3", done: false },
        { todo: "4", done: false },
      ],
    };
  },
  methods: {
    addItem() {
      this.todos.push({ todo: this.todo, done: false });
      this.todo = "";
    },
    removeTodo(todo) {
      const todoIndex = this.todos.indexOf(todo);
      this.todos.splice(todoIndex, 1);
    },
    reorderItems(todo) {
      if (todo.done) {
        // Move checked item to the bottom
        this.removeTodo(todo);
        this.todos.push(todo);
      } else {
        // Move unchecked item to the top
        this.removeTodo(todo);
        this.todos.unshift(todo);
      }
    },
  },
};
</script>
<style src="./ToDo.css" scoped></style>
