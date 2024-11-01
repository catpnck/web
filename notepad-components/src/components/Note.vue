<script>
export default {
  emits: [
    'edit',
    'delete',
  ],

  props: {
    note: Object,
  }
}
</script>

<template>
  <div class="note-block">
    <button class="note link" @click="$emit('edit', note.index)">{{ note.note }}</button>
    <button class="link" @click.prevent="$emit('delete', note.index)">X</button>
  </div>
</template>

<style scoped>
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

@media (hover: hover) {
  button.link:hover {
    background-color: hsla(160, 100%, 37%, 0.2);
  }
}
</style>