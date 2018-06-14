<template>
    <div>
        <ul class="ToDoList">
            <transition-group>
                <ToDoListItem
                    v-for="todo in undoneTodos" :key="todo.createdAt" :todo="todo"
                    v-on:done="toggleDone(todo)"
                ></ToDoListItem>
            </transition-group>
        </ul>
        <p v-if="!isEditing">
            <a href="javascript: void(0);" v-on:click="toggleEditing">Add another item</a>
        </p>
        <form v-else v-on:submit.prevent>
            <input type="text" v-model="content"/>
            <p>
                <button @click="addToDo">Add this item</button>
                <a href="javascript: void(0);" style="margin-left: 10px;" v-on:click="toggleEditing">Close</a>
            </p>
        </form>
        <ul class="ToDoList">
            <transition-group>
                <ToDoListItem
                    v-for="todo in doneTodos" :key="todo.createdAt" :todo="todo"
                    v-on:undone="toggleDone(todo)"
                ></ToDoListItem>
            </transition-group>
        </ul>
    </div>
</template>

<script>
import ToDoListItem from './ToDoListItem';

export default {
    name: 'ToDoList',
    data() {
        return {
            isEditing: false,
            content: '',
            todos: [],
        };
    },
    components: {
        ToDoListItem,
    },
    methods: {
        toggleEditing() {
            this.isEditing = !this.isEditing;
        },
        toggleDone(todo) {
            todo.isDone = !todo.isDone;
        },
        addToDo() {
            this.todos.push({
                content: this.content,
                createdAt: Date.now(),
                isDone: false,
            });
            this.content = '';
        },
    },
    computed: {
        undoneTodos() {
            return this.todos.filter((todo) => {
                return !todo.isDone;
            });
        },
        doneTodos() {
            return this.todos.filter((todo) => {
                return todo.isDone;
            });
        },
    },
};
</script>

<style>
.ToDoList {
    list-style: none;
    padding: 0;
}

.v-enter {
    background-color: rgba(255, 255, 153, 1);
}

.v-enter-to {
    background-color: rgba(255, 255, 153, 0);
}

.v-enter-active {
    transition: all 1.5s ease;
}
</style>
