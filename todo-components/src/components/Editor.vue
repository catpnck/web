<script>
export default {
    emits: [
        'save',
    ],

    props: {
        initialText: String,
    },

    watch: {
        initialText: function () {
            this.text = this.initialText
        }
    },
    
    data() {
        return {
            text: this.initialText
        }
    },

    methods: {
        save: function() {
            this.$emit('save', this.text)
            this.text = ""
        }
    }
}
</script>

<template>
    <textarea class="create-todo" v-model="text"></textarea>
    <button @click="save">{{ this.initialText ? "Сохранить" : "Добавить" }}</button>
</template>

<style>
textarea.create-todo {
    margin: 5px;
    resize: none;
}
</style>