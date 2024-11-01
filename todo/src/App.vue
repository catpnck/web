<script>
export default {
  data() {
    return {
      todoItems: [
      ],

      newTodoText: "",
      editTodoIndex: null
    }
  },

  methods: {
    removeTodo: function (index) {
      this.todoItems.splice(index, 1)
    },

    createTodo: function () {
      if (this.editTodoIndex != null) {
        var todoItem = this.todoItems[this.editTodoIndex]
        todoItem.text = this.newTodoText
      } else {
        this.todoItems.push({
          text: this.newTodoText,
          isDone: false,
        })
      }
      this.newTodoText = ""
      this.editTodoIndex = null
    },

    editTodo: function (index) {
      this.editTodoIndex = index
      this.newTodoText = this.todoItems[index].text
    }
  },

  computed: {
  },

  components: {
  }
}
</script>


<template>
  <template v-for="(todoItem, index) in todoItems">
    <div class="todo">
      <input type="checkbox" v-model="todoItem.isDone" class="todo-component checkbox" />
      <p :class="{ done: todoItem.isDone }" class="todo-component">{{ todoItem.text }} </p>
      <button @click="editTodo(index)" class="todo-component">Редактировать</button>
      <button @click="removeTodo(index)" class="todo-component">Удалить</button>
    </div>
  </template>

  <textarea class="create-todo" v-model="newTodoText"></textarea>
  <button @click="createTodo">{{ this.editTodoIndex != null ? "Сохранить" : "Добавить" }}</button>
</template>

<style>
p.done {
  text-decoration: line-through;
}

div.todo {
  display: grid;
  grid-template-columns: 1fr 5fr 1fr 1fr;
  margin: 10px;
}

.todo-component {
  padding: 3px;
  margin: 5px;
}

input.checkbox {
  aspect-ratio: 1;
  max-width: 30px;
}

textarea.create-todo {
  margin: 5px;
  resize: none;
}
</style>