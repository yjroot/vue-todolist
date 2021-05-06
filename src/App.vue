<template>
  <div id="app">
    <TodoHeader 
      v-on:addItem="addItem" />
    <TodoList 
      v-bind:propsdata="todoItems" 
      v-on:deleteItem="deleteItem"
      v-on:completeItem="completeItem"/>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoList from './components/TodoList.vue'

export default {
    data() {
        return {
            todoItems: []
        };
    },
    created() {
        if (localStorage.length > 0) {
            for(let i = 0;i < localStorage.length; i++) {
                if (localStorage.key(i) !== "loglevel:webpack-dev-server") {
                    this.todoItems.push(
                        JSON.parse(localStorage.getItem(localStorage.key(i)))
                    );
                }
            }
            
            this.todoItems.sort(function (a, b) {
              return Date.parse(a.date) - Date.parse(b.date);
            });
        }
    },
    methods: {
        addItem(todoItem) {
            console.log(todoItem);
            var date = new Date();
            var value = {
                item: todoItem,
                date: date.toString(),
                completed: false
            }
            localStorage.setItem(date.toString(), JSON.stringify(value));
            this.todoItems.push(value);
        },
        completeItem(todoItem) {
            todoItem.completed = !todoItem.completed;
            localStorage.setItem(todoItem.date, JSON.stringify(todoItem));
        },
        deleteItem(todoItem, index) {
            localStorage.removeItem(todoItem.date);
            this.todoItems.splice(index, 1);
        }
    },
    name: 'App',
    components: {
      TodoHeader,
      TodoList
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
