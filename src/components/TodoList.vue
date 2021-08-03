<template>
    <div>
        <input
            type="text"
            class="todo-input"
            placeholder="Введите задание"
            v-model="newTodo"
            @keyup.enter="addTodo">
        <div
            v-for="(todo, index) in todosFiltered"
            :key="todo.id"
            class="todo-item">
            <div class="todo-item__done">
                <input
                    type="checkbox"
                    v-model="todo.completed">
            </div>
            <div class="todo-item__title"
                 :class="{ completed : todo.completed}">
                {{ todo.title }}
            </div>
            <div
                class="todo-item__remove"
                @click="removeTodo(index)">
                <span>x</span>
            </div>
        </div>
        <div class="todo-remain">
            <div class="todo-remain__control">
                <div>
                    <input
                        type="checkbox"
                        class="todo-remain__input"
                        :checked="!anyRemaining"
                        @change="checkAllTodos">
                        <span>Выполнить все</span>
                </div>
                <div>
                    Заданий осталось - {{ remaining }}
                </div>
            </div>
            <div class="todo-remain__control">
                <div>
                    <button
                        :class="{ active: filter == 'all' }"
                        @click="filter = 'all'">
                        Все
                    </button>
                    <button
                        :class="{ active: filter == 'active' }"
                        @click="filter = 'active'">
                        Активные
                    </button>
                    <button
                        :class="{ active: filter == 'completed' }"
                        @click="filter='completed'">
                        Выполненные
                    </button>
                </div>
                <div>
                    <button
                        v-if="showClearCompletedButton"
                        @click="clearCompleted">
                        Очистить выполненные
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'TodoList',
        data () {
            return {
                newTodo: '',
                idForTodo: 3,
                filter: 'all',
                todos: [
                    {
                        'id': 1,
                        'title': 'Проснуться',
                        'completed': false,
                    },
                    {
                        'id': 2,
                        'title': 'Приготовить кофе',
                        'completed': false,
                    },
                ]
            }
        },
        computed: {
            remaining() {
                return this.todos.filter(todo => !todo.completed).length
            },
            anyRemaining() {
                return this.remaining != 0
            },
            todosFiltered() {
                if (this.filter == 'all') {
                    return this.todos
                } else if (this.filter == 'active') {
                    return this.todos.filter(todo => !todo.completed)
                } else if (this.filter == 'completed') {
                    return this.todos.filter(todo => todo.completed)
                }
                return this.todos
            },
            showClearCompletedButton() {
                return this.todos.filter(todo => todo.completed).length > 0
            }
        },
        methods: {
            addTodo() {

                if (this.newTodo.trim().length == 0){
                    return
                }

                this.todos.push({
                    id: this.idForTodo,
                    title: this.newTodo,
                    completed: false,
                })

                this.newTodo = ''
                this.idForTodo++
            },
            removeTodo(index) {

                this.todos.splice(index, 1)

            },
            checkAllTodos() {
                this.todos.forEach((todo) => todo.completed =
                event.target.checked)
            },
            clearCompleted() {
                this.todos = this.todos.filter(todo => !todo.completed)
            }
        }
    }
</script>

<style>
    .todo-input{
        width: 100%;
        padding: 10px 18px;
        font-size: 16px;
        margin-bottom: 16px;
    }
    .todo-input:focus{
        outline: 0;
    }

    .todo-item{
        display: flex;
        align-items: center;
        margin-bottom: 12px;
    }

    .todo-item__title.completed{
        text-decoration: line-through;
        color: grey;
    }

    .todo-item__title{
        flex: 1 1 auto;
        padding: 0 10px;
    }

    .todo-item__remove{
        cursor: pointer;
    }
    .todo-item__remove:hover{
        color: red;
    }

    .todo-remain__input{
        margin-right: 10px;
    }

    .todo-remain__control{
        display: flex;
        align-items: center;
        justify-content: space-between;
    }

    .todo-remain__control span{
        font-size: 12px;
    }
</style>