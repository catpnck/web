<!-- Основная компонента приложения -->
<script>
import TodoItem from './components/TodoItem.vue';
import Editor from './components/Editor.vue';

export default {
  data() {
    return {
      todoItems: [ // Значения todo
      ],

      editTodoIndex: null, // текущая редактируемая todo
      editTodoText: "", // Текст редактируемой todo
    }
  },

  methods: {
    // Метод, помечающий todo сделанной
    markAsDone: function (index, isDone) {
      this.todoItems[index].isDone = isDone
    },

    // Метод, удаляющий todo
    remove: function (index) {
      this.todoItems.splice(index, 1)
    },

    // Метод, сохраняющий новую или измененную todo
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

    // Метод, проставляющий изменяемую todo
    edit: function (index) {
      this.editTodoIndex = index
      this.editTodoText = this.todoItems[index].text
    }
  },

  // Компоненты, используемые в приложении
  components: {
    TodoItem,
    Editor,
  }
}
</script>


<!-- Шаблон, создающий компоненты TodoItem для каждой todo и редактор -->
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
