<!-- Компонента поиска (поискаовая строка) -->

<script>
export default {
    // Событие, генерируемое строкой поиска при изменении значения в ней
    emits: [
        'onTextChanged'
    ],

    // Данные, котрые хранят текст, введенный в поле поиска
    data() {
        return {
            text: "",
        }
    },

    // "Слушатель" изменения значения text и вызывающий событие при его изменении
    watch:
    {
        text(newValue, oldValue) {
            if (newValue !== oldValue) 
                this.$emit('onTextChanged', newValue);
        }
    },
}
</script>

<template>
    <input class="search" type="text" placeholder="Поиск" v-model="text"></input>
</template>

<style scoped>
input.search {
  width: 80%;
}
</style>