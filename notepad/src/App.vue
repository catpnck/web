<script>
export default {
  data() {
    return {
      notes: [],
      editedNote: "",
      editedNoteId: null,
      searchText: "",
    }
  },

  methods: {
    saveNote: function () {
      if (!this.editedNote) {
        return
      }
      if (this.editedNoteId == null) {
        this.notes.push(this.editedNote)
      } else {
        this.notes[this.editedNoteId] = this.editedNote
      }
      this.editedNote = ""
      this.editedNoteId = null
    },

    onEdit: function (index) {
      this.editedNoteId = index
      this.editedNote = this.notes[index]
    },

    onDelete: function (index) {
      this.notes.splice(index, 1)
      this.editedNoteId = null
      this.editedNote = ""
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
    <input class="search" type="text" placeholder="Поиск" v-model="searchText"></input>
    <template v-for="noteObj in filteredNotes">
      <div class="note-block">
        <button class="note link" @click="onEdit(noteObj.index)">{{ noteObj.note }}</button>
        <button class="link" @click.prevent="onDelete(noteObj.index)">X</button>
      </div>
    </template>
  </div>
  <div>
    <textarea class="editor" v-model="editedNote"></textarea>
    <button @click="saveNote">Сохранить</button>
  </div>
</template>

<style scoped>
textarea.editor {
  width: 100%;
  height: 80%;
}

button.note {
  color: black !important;
  line-height: 1.8em;
  max-height: 1.8em;
  overflow: hidden;
  text-overflow: ellipsis;
  text-align: left;
}

button.link {
  text-decoration: none;
  color: hsla(160, 100%, 37%, 1);
  transition: 0.4s;
  padding: 3px;
  cursor: default;
  border: none;
  background: none;
}

.note-block {
  display: grid;
  grid-template-columns: 8fr 1fr;
}

input.search {
  width: 80%;
}

@media (hover: hover) {
  button.link:hover {
    background-color: hsla(160, 100%, 37%, 0.2);
  }
}
</style>
