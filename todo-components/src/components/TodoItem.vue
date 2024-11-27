<!-- Компонента одной todo -->
<script>
export default {
    // События, генерируемые компонентой: отметка о выполнении, редактирование и удаление
    emits: [
        'done',
        'edit',
        'delete',
    ],

    props: {
        text: String, // текст todo
        isDone: Boolean, // флаг, обозначающий выполнение
        id: Number, // id todo
    },
}
</script>

<!-- Шаблон, размещающий текст заметки, чекбокс выполнения и кнопки редактирования/удаления -->
<template>
    <div class="todo">
        <!-- :checked связывает состояния чекбокса с isDone -->
        <input type="checkbox" :checked="isDone" @click="$emit('done', id, !isDone)" class="todo-component checkbox" />
        <!-- Используем conditional класс для перечеркивания заметки при отмеченном чекбоксе -->
        <p :class="{ done: isDone }" class="todo-component">{{ text }} </p>
        <button @click="$emit('edit', id)" class="todo-component">Редактировать</button>
        <button @click="$emit('delete', id)" class="todo-component">Удалить</button>
    </div>
</template>

<style>
/* Стиль, перечеркивающий выполненную todo */
p.done {
    text-decoration: line-through;
}

/* Задание относительных размеров колонок для элементов компоненты */
div.todo {
    display: grid;
    grid-template-columns: 1fr 5fr 1fr 1fr;
    margin: 10px;
}

/* Стиль, задающий поля и отступы для текста заметки */
.todo-component {
    padding: 3px;
    margin: 5px;
}

/* Стиль чекбокса, задающий максимальную ширину чекбокса и отношение сторон */
input.checkbox {
    aspect-ratio: 1;
    max-width: 30px;
}
</style>