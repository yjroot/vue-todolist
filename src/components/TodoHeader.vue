<template lang="">
    <header class="TodoHeader">
        <h1> Just To-Do List </h1>
        <div class="TodoInput">
            <input 
                id="todo-input"
                type="text" 
                placeholder="Enter" 
                v-model="newTodoItem"
                v-on:keyup.enter="addTodoItem">
            <button 
                id="todo-add-button"
                v-on:click="addTodoItem">Add</button>
        </div>
    </header>
</template>
<script>
export default {
    data() {
        return {
            newTodoItem: ""
        };
    },
    methods: {
        addTodoItem() {
            if(this.newTodoItem !== "") {
                this.$emit("addItem", this.newTodoItem);
                this.clearInput();
            }  
        },
        clearInput() {
            this.newTodoItem = "";
        }
    },
    name: "TodoHeader",
}
</script>
<style lang="scss">
    .TodoHeader {
        max-width: 960px;
        min-height: 72px;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        text-align: center;

        margin: 0 auto;
        background-color: #D9AFD9;
        background-image: linear-gradient(0deg, #D9AFD9 0%, #97D9E1 100%);
        color: white;
    }
    .TodoInput {
        width: 100%;
        padding: 10px 0px 10px 0px;
    }
    #todo-input {
        width: 80%;
    }
</style>