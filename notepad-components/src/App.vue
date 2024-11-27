<script>
import Note from './components/Note.vue'
import Editor from './components/Editor.vue'
import Search from './components/Search.vue'

export default {
  // Данные, используемые в приложении на главной странице
  data() {
    return {
      notes: [], // Список заметок
      editedNoteId: null, // Текущая редактируемая заметка
      searchText: "", // Текст в поле поиска
    }
  },

  // Компоненты, используемые на страницу
  components: {
    Note,
    Editor,
    Search,
  },

  methods: {
    // Метод, сохраняющий заметку (новую или отредактированную)
    saveNote: function (text) {
      if (!text) {
        return
      }
      if (this.editedNoteId == null) {
        this.notes.push(text)
      } else {
        this.notes[this.editedNoteId] = text
      }
      this.editedNoteId = null
    },

    // Метод, устанавливающий текущую редактируемую заметку
    onEdit: function (index) {
      this.editedNoteId = index
    },

    // Метод, удаляющий заметку
    onDelete: function (index) {
      this.notes.splice(index, 1)
      this.editedNoteId = null
    },

    // Метод, реагирующий на изменение текста в поле поиска
    onSearch: function (text) {
      this.searchText = text
    }
  },

  // computed-свойства, вычисляющее отфильтрованные заметки
  computed: {
    filteredNotes: function () {
      var filtered = []

      for (var i = 0; i < this.notes.length; i++) {
        var note = this.notes[i]
        if (!this.searchText || note.includes(this.searchText)) {
          filtered.push({
            note: note,
            index: i
          })
        }
      }

      return filtered
    }
  }
}
</script>

<!-- Шаблон страницы, располагающий компоненты на странице -->
<template>
  <div>
    <Search @onTextChanged="onSearch" />
    <!-- Проставляем подписки на события для компоненты заметки и передаем объекты. Генерируем Note для каждой сохраненной заметки -->
    <Note v-for="noteObj in filteredNotes" :note="noteObj" @edit="onEdit" @delete="onDelete" />
  </div>
  <div>
    <Editor :initialText="this.notes[editedNoteId]" @save="saveNote" />
  </div>
</template>
