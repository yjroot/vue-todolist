<template lang="">
    <main class="TodoList">
        <div class="TodoListItem" v-for="(todoItem, index) in todoItems" v-bind:key="todoItem.time">
            <div class="leftBox">
                <input
                    type="checkbox"
                    v-bind:id="todoItem.item"
                    v-bind:checked="todoItem.completed === true"
                    v-on:change="completeTodoItem(todoItem)"/>
                <div 
                    class="TodoListItemLabel"  
                    v-on:click="completeTodoItem(todoItem)">
                    <label> 
                        {{todoItem.item}}
                    </label>
                </div>
            </div>
            
            <div>
                <button 
                    id="todo-del-button"
                    v-on:click="deleteTodoItem(todoItem, index)">Delete</button>
            </div>
        </div>
    </main>
</template>
<script>
export default {
    props: ["todoItems"],
    methods: {
        completeTodoItem(todoItem) {
            this.$emit("completeItem", todoItem);
        },
        deleteTodoItem(todoItem, index) {
            this.$emit("deleteItem", todoItem, index);
        }
    }
}
</script>
<style lang="scss">
    .TodoList {
        width: 100%;
        max-width: 960px;
        padding-bottom: 72px;
        
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        text-align: center;
    }
    .TodoListItem {
        width: 100%;
        min-height: 32px;
        display: flex;
        justify-content: center;
        align-items: center;
        background-color: #D9AFD9;
    }
    .leftBox {
        width: 80%;
        display: flex;
        flex-direction: row;
        justify-content: center;
        text-align: center;
        align-items: center;
    }
    .TodoListItemLabel {
        width: 95%;
        min-height: 48px;
        display: flex;
        justify-content: center;
        align-items: center;
        text-align: center;
    }
</style>
