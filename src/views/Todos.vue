<template>
    <div>
        <h2>Todo app</h2>
        <router-link to='/'>Home</router-link>
        <Loader v-if='loading'/>
        <TodoList 
        v-else-if="filteredTodos.length"
        v-bind:todos='filteredTodos'
        v-on:remove-todo='removeTodo'
        />
        <p v-else>No todos!</p>
        <select v-model="filter">
            <option value="all">All</option>
            <option value="completed">Completed</option>
            <option value="non-completed">Non-completed</option>
        </select>
        <AddTodo 
        v-bind:todos='todos'
        v-on:add-todo='addTodo'
        />  
    </div>
</template>

<script>
import TodoList from '@/components/TodoList'
import AddTodo from '@/components/AddTodo'
import Loader from '@/components/Loader'
export default {
    name: 'App',
    data() {
        return {
            todos: [
                {id: 1, title: 'Make notes', completed: false},
                {id: 2, title: 'Make todos', completed: false},
                {id: 3, title: 'Send project', completed: false}
            ],
            loading: false,
            filter: 'all'
        }
    },
    components: {
        TodoList, AddTodo, Loader
    },
    computed: {
        filteredTodos() {
           if (this.filter === 'completed') {
                return this.todos.filter(todo=>todo.completed)
            } else if (this.filter === 'non-completed') {
                return this.todos.filter(todo=>!todo.completed);
            }
            return this.todos
        }
    },
    methods: {
        removeTodo(id) {
            this.todos = this.todos.filter(todo => todo.id!==id)
        },
        addTodo(todo) {
            this.todos.push(todo)
        }
    }
}

</script>