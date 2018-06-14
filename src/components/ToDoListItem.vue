<template>
    <li :class="{'ToDoItem--Done': todo.isDone}">
        <input type="checkbox" @change="onChange" :checked="todo.isDone">
        {{ todo.content }}
    </li>
</template>

<script>
export default {
    name: 'ToDoListItem',
    props: ['todo'],
    methods: {
        onChange() {
            if (this.todo.isDone) {
                // 未完了にするようにイベントを発火
                this.$emit('undone');
            } else {
                // 完了にするようにイベントを発火
                this.$emit('done');
            }
        }
    }
};
</script>

<style>
.ToDoItem--Done {
    font-size: 10px;
    color: #999;
}
</style>