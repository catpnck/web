<script>
import Note from './components/Note.vue'
import Editor from './components/Editor.vue'
import Search from './components/Search.vue'

export default {
  data() {
    return {
      notes: [],
      filteredNotes: [],
      editedNoteId: null,
      searchText: "",
    }
  },

  components: {
    Note,
    Editor,
    Search,
  },

  methods: {
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

    onEdit: function (index) {
      this.editedNoteId = index
    },

    onDelete: function (index) {
      this.notes.splice(index, 1)
      this.editedNoteId = null
    },

    onSearch: function (text) {
      this.searchText = text
    }
  },

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

<template>
  <div>
    <Search @onTextChanged="onSearch" />
    <Note v-for="noteObj in filteredNotes" :note="noteObj" @edit="onEdit" @delete="onDelete" />
  </div>
  <div>
    <Editor :initialText="this.notes[editedNoteId]" @save="saveNote" />
  </div>
</template>
