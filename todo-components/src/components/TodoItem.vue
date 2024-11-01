<script>
export default {
    emits: [
        'done',
        'edit',
        'delete',
    ],

    props: {
        text: String,
        isDone: Boolean,
        id: Number,
    },
}
</script>

<template>
    <div class="todo">
        <input type="checkbox" :checked="isDone" @click="$emit('done', id, !isDone)" class="todo-component checkbox" />
        <p :class="{ done: isDone }" class="todo-component">{{ text }} </p>
        <button @click="$emit('edit', id)" class="todo-component">Редактировать</button>
        <button @click="$emit('delete', id)" class="todo-component">Удалить</button>
    </div>
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
</style>