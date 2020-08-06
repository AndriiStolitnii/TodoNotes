<template>
    <form v-on:submit.prevent='onSubmit'>
        <input type='text' v-model='title'>
        <button type='submit'>Create</button>
    </form>
</template>

<script>
export default {
    props: ['todos'],
    data() {
        return {
            title: ''
        }
    },
    methods: {
        onSubmit() {
            if(this.title.trim()) {
                const newTodo = {
                    id: this.todos.length > 0 ? Math.max(...this.todos.map(todo=>todo.id))+1 : 1,
                    title: this.title,
                    completed: false
                }
                this.$emit('add-todo', newTodo)
                this.title=''
            }
        }
    }
}
</script>

<style scoped>
    form {
        display: flex;
    }

    input {
        width: 400px;
    }
</style>