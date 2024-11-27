<!-- Коммпонента редактора заметки -->

<script>
export default {
    // События, которые генерирует компонента
    emits: [
        'save',
    ],

    // prop, принимающий значение редактируемой заметки
    props: {
        initialText: String,
    },

    // "слушатель" изменения initialText
    watch: {
        initialText: function () {
            this.text = this.initialText
        }
    },

    // Данные, используемые в компоненте
    data() {
        return {
            text: this.initialText
        }
    },

    // Метод save, вызывающий событие сохранения
    methods: {
        save: function () {
            this.$emit('save', this.text)
            this.text = ""
        }
    }
}
</script>

<!-- Шаблон компоненты, содержащий поле для ввода текста и кнопку Сохранить -->
<template>
    <textarea class="editor" v-model="text"></textarea>
    <button @click="save">Сохранить</button>
</template>

<!-- Стили, задающие размеры редактора текста -->
<style scoped>
textarea.editor {
    width: 100%;
    height: 80%;
}
</style>