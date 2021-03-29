<template>
    <div>
        <ul>
            <TodoItem
                v-for="(todo, i) of todos"
                v-bind:index='i'
                v-bind:todo='todo'
                v-on:remove-todo="removeTodo"
            />
        </ul>
    </div>
</template>

<script>
import TodoItem from '@/components/TodoItem'
export default {
    props: ['todos'],
    components: {
        TodoItem
    },
    methods: {
        removeTodo(id) {
            this.$emit('remove-todo', id)
        }
    }
}
</script>

<style scoped>
    ul {
        padding: 0;
        margin: 0;
        list-style: none;
    }
</style>