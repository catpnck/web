<!-- Компонента редактора todo -->

<script>
export default {
    // Событие сохранения, генерируемое компонентой
    emits: [
        'save',
    ],

    // text, проставляемый в поле редактирования
    props: {
        initialText: String,
    },

    // "Слушатель" изменения текста в редакторе
    watch: {
        initialText: function () {
            this.text = this.initialText
        }
    },
    
    // Данные, используемые компонентой
    data() {
        return {
            text: this.initialText
        }
    },

    methods: {
        // Метод сохранения, вызывающий событие сохранения для родительской компоненты
        save: function() {
            this.$emit('save', this.text)
            this.text = ""
        }
    }
}
</script>

<!-- Шаблон, размешающий поле ввода и кнопку сохранения -->
<template>
    <textarea class="create-todo" v-model="text"></textarea>
    <button @click="save">{{ this.initialText ? "Сохранить" : "Добавить" }}</button>
</template>

<!-- Стиль для поля ввода, задающий поля и запрещающий изменение размеров -->
<style>
textarea.create-todo {
    margin: 5px;
    resize: none;
}
</style>