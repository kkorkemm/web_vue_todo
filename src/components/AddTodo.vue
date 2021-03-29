<template>
    <form @submit.prevent='onSubmit'>
        <input type="text" v-model="title">
        <button type="submit">Create</button>
    </form>
</template>

<script>
export default {
    data() {
        return {
            title: ''
        }
    },
    methods: {
        onSubmit() {
            if (this.title.trim()) {
                const newTodo = {
                    id: Date.now(),
                    title: this.title,
                    completed: false
                }
                this.$emit('add-todo', newTodo)
                this.title = ''
            }
        }
    }
}
</script>

<style scoped>
    form {
        display: flex;
        margin: 20px auto 0;
        width: 300px;
        justify-content: space-between;
    }
    button {
        cursor: pointer;
        border: none;
        border-radius: 5px;
        padding: 0 15px;
        font-size: .9rem;
    }
    input {
        outline: none;
        font-size: 1rem;
        border-radius: 5px;
        border: 1px #000 solid;
        padding: 3px 5px;
    }
</style>