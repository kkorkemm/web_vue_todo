<template>
    <li>
        <span v-bind:class="{done: todo.completed}">
            <input type="checkbox" v-on:change="todo.completed=!todo.completed">
            <strong>{{index + 1}}</strong>
            {{todo.title | uppercase}}
        </span>
        <button class="remove-btn" v-on:click="$emit('remove-todo', todo.id)">&times;</button>
    </li>
</template>

<script>
export default {
    props: {
        todo: {
            type: Object,
            required: true
        },
        index: Number
    },
    filters: {
        uppercase(value) {
            return value.toUpperCase()
        }
    }
}
</script>

<style scoped>
    input {
        margin-right: 1rem;
    }
    li {
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: .7rem;
        background: rgba(199, 238, 226, 0.466);
        border-radius: 10px;
    }
    li + li {
        margin-top: 10px;
    }
    .remove-btn {
        border: none;
        border-radius: 50%;
        background: rgb(255, 137, 137);
        color: rgb(228, 228, 228);
        font-size: 1.2rem;
        display: block;
        width: 30px;
        height: 30px;
        outline: none;
        cursor: pointer;
    }
    .done {
        text-decoration: line-through;
    }
</style>