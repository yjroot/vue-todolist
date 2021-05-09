<template>
  <div id="app">
    <TodoHeader 
      v-on:addItem="addItem" />
    <TodoList 
      v-bind:propsdata="todoItems" 
      v-on:deleteItem="deleteItem"
      v-on:completeItem="completeItem"/>
    <TodoFooter 
      v-on:clearItem="clearItem"/>
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
        if (localStorage.length > 0) {
            // Push to-do items in local storage to todoItems array.
            for(let i = 0;i < localStorage.length; i++) {
                if (localStorage.key(i) !== "loglevel:webpack-dev-server") {
                    this.todoItems.push(
                        JSON.parse(localStorage.getItem(localStorage.key(i)))
                    );
                }
            }
            
            // Sort to-do items by time (oldest to latest).
            this.todoItems.sort(function (a, b) {
              return a.time - b.time;
            });
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
            // console.log(date.getTime().toString(), value);
            localStorage.setItem(date.getTime().toString(), JSON.stringify(value));
            this.todoItems.push(value);
        },
        completeItem(todoItem) {
            // Reverse the completed property
            todoItem.completed = !todoItem.completed;
            localStorage.setItem(todoItem.time, JSON.stringify(todoItem));
        },
        deleteItem(todoItem, index) {
            // Delete to-do item
            localStorage.removeItem(todoItem.time);
            this.todoItems.splice(index, 1);
        },
        clearItem() {
            localStorage.clear();
            this.todoItems = [];
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
