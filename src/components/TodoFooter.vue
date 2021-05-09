<template lang="">
    <div>
        <footer class="TodoFooter">
            <button 
                id="todo-clear-button"
                v-on:click="clearTodoItem">Clear</button>
        </footer>
    </div>
</template>
<script>
export default {
    name: "TodoFooter",
    methods: {
        clearTodoItem() {
                this.$emit("clearItem");
        }
    }
}
</script>
<style lang="scss">
    .TodoFooter {
        width: 100%;
        height: 72px;
        max-width: 960px;

        position: fixed;
        left: 0;
        right: 0;
        bottom: 0;
        
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        text-align: center;

        margin: 0 auto;
        background-color: #D9AFD9;
        background-image: linear-gradient(0deg, #97D9E1 0%, #D9AFD9 100%);
        color: white;
    }
</style>