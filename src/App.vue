<template>
  <div id="app">
    <TodoHeader 
      @addItem="addItem" />
    <TodoList 
      :todoItems="todoItems" 
      @deleteItem="deleteItem"
      @completeItem="completeItem"/>
    <TodoFooter 
      @clearItem="clearItem"/>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoFooter from './components/TodoFooter.vue'
import TodoList from './components/TodoList.vue'

export default {
    data() {
        return {
            todoItems: []
        };
    },
    created() {
        const todoItemsJson = localStorage.getItem('todoItems')
        if (todoItemsJson) {
            try {
              this.todoItems = JSON.parse(todoItemsJson)
            } catch (e) {
              alert('error: localStorage')
            }
        }
    },
    methods: {
        addItem(todoItem) {
            // Create to-do item
            // key : time
            // value : {item, date, time, completed}
            var date = new Date();
            var value = {
                item: todoItem,
                date: date.toString(),
                time: date.getTime(),
                completed: false
            }
            this.todoItems.push(value);
            this.save()
        },
        completeItem(todoItem) {
            // Reverse the completed property
            todoItem.completed = !todoItem.completed;
            this.save()
        },
        deleteItem(todoItem, index) {
            // Delete to-do item
            this.todoItems.splice(index, 1);
            this.save()
        },
        clearItem() {
            this.todoItems = [];
            this.save()
        },
        save() {
            localStorage.setItem('todoItems', JSON.stringify(this.todoItems));
        }
    },
    name: 'App',
    components: {
      TodoHeader,
      TodoList,
      TodoFooter,
    },
}
</script>

<style lang="scss">
#app {
    min-height: 100%;
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
  
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    text-align: center;
}
input, button {
    font-size: 16px;
}
input {
    outline: none;
    border: 0;
    background: transparent;
}
button {
    border: none;
    border-radius: 5px;
    background: rgba(151, 217, 225, 0.3);
    color:white;
}
</style>
