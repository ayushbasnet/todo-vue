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
          <li v-for="(todos, index) in todos" :key="todos.id">
            <input
              type="checkbox"
              id="checkbox1"
              v-model="todos.checked"
              @change="reorderItems(todos, index, (top = true))"
            />
            <span :class="{ checked: todos.checked }"> {{ todos.todo }}</span>
            <button @click="removeTodo(todos)" type="button" name="button">
              Remove
            </button>
          </li>
        </transition-group>
      </ul>
      <h3>Completed Tasks</h3>
      <ul>
        <transition-group
          name="list2"
          enter-active-class="animated bounceInUp"
          leave-active-class="animated bounceOutDown"
        >
          <li v-for="(todos, index) in todosDone" :key="todos.id">
            <input
              type="checkbox"
              id="checkbox2"
              v-model="todos.checked"
              @change="reorderItems(todos, index, (top = false))"
            />
            <span :class="{ checked: todos.checked }"> {{ todos.todo }}</span>
            <button @click="removeTodoDone(todos)" type="button" name="button">
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
      counter: 6,
      todos: [
        { id: 1, todo: "1", checked: false },
        { id: 2, todo: "2", checked: false },
        { id: 3, todo: "3", checked: false },
        { id: 4, todo: "4", checked: false },
      ],
      todosDone: [
        { id: 5, todo: "1", checked: true },
        { id: 6, todo: "2", checked: true },
      ],
    };
  },
  methods: {
    addItem() {
      this.todos.push({ todo: this.todo, checked: false, id: this.counter++ });
      this.todo = "";
    },
    removeTodo(todo) {
      const todoIndex = this.todos.indexOf(todo);
      this.todos.splice(todoIndex, 1);
    },
    removeTodoDone(todo) {
      const todoIndex = this.todosDone.indexOf(todo);
      this.todosDone.splice(todoIndex, 1);
    },
    reorderItems(todo, index, top) {
      if (top) {
        if (todo.checked) {
          // Move checked item to the bottom
          this.todos.splice(index, 1);

          this.todosDone.push(todo);
        }
      } else {
        // Move unchecked item to the top
        if (!todo.checked) {
          this.todosDone.splice(index, 1);

          this.todos.push(todo);
        }
      }
    },
  },
};
</script>
<style src="./ToDo.css" scoped></style>
