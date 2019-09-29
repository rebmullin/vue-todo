<template>
  <div>
    <md-field>
      <md-input
        v-model="currentTodo"
        @keydown.enter="addTodo()"
        placeholder="Add a todo"
      />
    </md-field>
    <ul class="todos">
      <li
        :class="{ editing: todo.id === editedToDoId }"
        v-for="todo in todos"
        :key="todo.id"
      >
        <div class="md-card">
          <div class="md-card-header md-card-header-flex">
            <div class="md-display-3" @dblclick="toggleCompleted(todo)">
              {{ todo.label }}
            </div>
          </div>

          <div class="md-card-content">
            <div class="md-checkbox">
              <input
                type="checkbox"
                @change="toggleCompleted(todo)"
                :checked="todo.completed"
              />

              <div class="md-checkbox-label">
                <strong>completed :</strong>
                <span class="">&nbsp;{{ todo.completed }}</span>
              </div>
            </div>
          </div>

          <div class="md-card-actions md-alignment-right">
            <button class="md-button md-raised" @click="removeTodo(todo)">
              <span class="md-button__label">Delete</span>
            </button>
          </div>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todos: [],
      currentTodo: "",
      editedToDoId: ""
    };
  },
  methods: {
    addTodo() {
      this.todos.push({
        id: this.todos.length,
        label: this.currentTodo,
        completed: false
      });
      this.currentTodo = "";
    },
    removeTodo(todo) {
      var index = this.todos.indexOf(todo);
      this.todos.splice(index, 1);
    },
    toggleCompleted(todo) {
      todo.completed = !todo.completed;
    }
  }
};
</script>

<style>
.editing {
  display: none;
}
</style>
