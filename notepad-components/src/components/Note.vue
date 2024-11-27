<!-- Компонента одной сохраненной заметки -->
<script>
export default {
  // События, генерируемые компонентой
  emits: [
    'edit',
    'delete',
  ],

  // prop, приинимающий текст заметки
  props: {
    note: Object,
  }
}
</script>

<!-- Шаблон, содержащий две кнопки: одну с текстом заметки, вызывающую ее редактирование, вторая - кнопка удаления -->
<template>
  <div class="note-block">
    <button class="note link" @click="$emit('edit', note.index)">{{ note.note }}</button>
    <button class="link" @click.prevent="$emit('delete', note.index)">X</button>
  </div>
</template>

<style scoped>
/* Стиль кнопки с текстом заметки. Задаем цвет текста, высоту, скрываем свойство overflow, добавляем обрезание текста (text-overflow), выравниваем по левому краю */
button.note {
  color: black !important;
  line-height: 1.8em;
  max-height: 1.8em;
  overflow: hidden;
  text-overflow: ellipsis;
  text-align: left;
}

/* Общий стиль кнопок, задающий цвета, анимацию и убирающий рамки и фон */
button.link {
  text-decoration: none;
  color: hsla(160, 100%, 37%, 1);
  transition: 0.4s;
  padding: 3px;
  cursor: default;
  border: none;
  background: none;
}

/* Выравниваем текст заметки */
.note-block {
  display: grid;
  grid-template-columns: 8fr 1fr;
}

/* Изменение цвета кнопок при наведении */
@media (hover: hover) {
  button.link:hover {
    background-color: hsla(160, 100%, 37%, 0.2);
  }
}
</style>