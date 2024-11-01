<script>
import TodoItem from './components/TodoItem.vue';
import Editor from './components/Editor.vue';

export default {
  data() {
    return {
      todoItems: [
      ],

      editTodoIndex: null,
      editTodoText: "",
    }
  },

  methods: {
    markAsDone: function (index, isDone) {
      this.todoItems[index].isDone = isDone
    },

    remove: function (index) {
      this.todoItems.splice(index, 1)
    },

    save: function (text) {
      if (this.editTodoIndex != null) {
        var todoItem = this.todoItems[this.editTodoIndex]
        todoItem.text = text
      } else {
        this.todoItems.push({
          text: text,
          isDone: false,
        })
      }
      this.editTodoIndex = null
      this.editTodoText = null
    },

    edit: function (index) {
      this.editTodoIndex = index
      this.editTodoText = this.todoItems[index].text
    }
  },

  components: {
    TodoItem,
    Editor,
  }
}
</script>


<template>
  <template v-for="(todoItem, index) in todoItems">
    <TodoItem 
      :text="todoItem.text" 
      :isDone="todoItem.isDone" 
      :id="index" 
      @done="markAsDone" 
      @edit="edit"
      @delete="remove" />
  </template>

  <Editor :initialText="editTodoText" @save="save"/>
</template>
