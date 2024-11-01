<script>
export default {
    emits: [
        'onTextChanged'
    ],

    data() {
        return {
            text: "",
        }
    },

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