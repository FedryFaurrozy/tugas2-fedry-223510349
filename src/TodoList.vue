<template>
  <div class="todo-list">
    <input
      type="text"
      placeholder="Tambah kegiatan..."
      v-model="newTodo"
      @keydown.enter="addTodo"
    />
    <div class="filter-container">
      <label for="filter-all">Semua</label>
      <input
        type="radio"
        id="filter-all"
        name="filter"
        v-model="filter"
        value="all"
        checked
      />
      <label for="filter-pending">Belum Selesai</label>
      <input
        type="radio"
        id="filter-pending"
        name="filter"
        v-model="filter"
        value="pending"
      />
    </div>
    <ul>
      <todo-item
        v-for="(todo, index) in filteredTodos"
        :key="index"
        :todo="todo"
        @toggle-done="toggleDone(index)"
        @delete-todo="deleteTodo(index)"
      />
    </ul>
  </div>
</template>

<script>
import TodoItem from "./TodoItem.vue";

export default {
  components: {
    TodoItem,
  },
  data() {
    return {
      todos: [
        { id: 1, text: "Belajar VueJS", done: false },
        { id: 2, text: "Membangun aplikasi to-do", done: false },
        { id: 3, text: "Minum kopi", done: true },
      ],
      newTodo: "",
      filter: "all",
    };
  },
  computed: {
    filteredTodos() {
      if (this.filter === "all") {
        return this.todos;
      } else {
        return this.todos.filter((todo) => !todo.done);
      }
    },
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim()) {
        this.todos.push({ id: Date.now(), text: this.newTodo, done: false });
        this.newTodo = "";
      }
    },
    toggleDone(index) {
      this.todos[index].done = !this.todos[index].done;
    },
    deleteTodo(index) {
      this.todos.splice(index, 1);
    },
  },
};
</script>

<style scoped>
.todo-list {
  list-style: none;
  padding: 0;
  margin: 0;
}

.todo-list li {
  display: flex;
  align-items: center;
  padding: 10px;
  border-bottom: 1px solid #ccc;
}

.todo-list .completed {
  text-decoration: line-through;
  color: #aaa;
}

.filter-container {
  display: flex;
  margin-bottom: 10px;
}

.filter-container label {
  margin-right: 10px;
}
</style>
