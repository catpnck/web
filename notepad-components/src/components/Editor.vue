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
        save: function () {
            this.$emit('save', this.text)
            this.text = ""
        }
    }
}
</script>

<template>
    <textarea class="editor" v-model="text"></textarea>
    <button @click="save">Сохранить</button>
</template>

<style scoped>
textarea.editor {
    width: 100%;
    height: 80%;
}
</style>