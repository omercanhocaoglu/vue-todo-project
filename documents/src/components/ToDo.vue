<template>
    <div class="height100 columns is-centered" :class="theme === `light` ? `lightTheme` : `darkTheme`">
        <div class="column is-4 has-text-centered mt-5">
            <span v-if="theme === `dark`" class="floatRight" @click="changeTheme"> <i class="fa-regular fa-lightbulb"> </i> </span>
            <span v-else="theme === `light`" class="floatRight" @click="changeTheme"> <i class="fa-regular fa-moon"> </i> </span>
            <!-- change theme icons will be above -->

            <h1 class="is-family-sans-serif is-size-2">  ToDo List App </h1>
            <form @submit.prevent="addTodo">
                <input class="input is-normal" type="text" placeholder="Text Here!" id="textInput" v-model="todo">
                <br> <br>
                <button class="button is-link" type="submit">Add</button>
            </form>
            <br>
            <div id="notification" v-for="todo in todos" :key="todo.id" class="notification is-link is-light" v-show="todo.content !== ``">
                <button class="delete" @click="deleted(todo)"></button>
                <span id="contentSpan" class="pointer has-text-black" @click="done(todo)" :class="{done: todo.done}"> 
                    {{ todo.content }} 
                </span>
            </div>
           
            <!-- information will be below -->
            <div class="icon-text">
                <span class="icon has-text-info">
                    <i class="fas fa-info-circle"></i>
                </span>
                <span>Information</span>
            </div>
            <p class="block has-text-left mt-3">
                Add an item to list what you want to add.  
            </p>
            <p class="block has-text-left has-text-danger">
                Cannot add an empty item!
            </p>
            <p class="block has-text-left">
                Make the item with <strong> click over item</strong>.
            </p>
            <p class="block has-text-left">
                Delete the item with <strong> click over <button class="delete"> </button> button</strong>.
            </p>
            <p class="block has-text-left">
                Change the theme with 
                    <strong>
                        <i class="fa-regular fa-lightbulb"></i> &nbsp;
                        <i class="fa-regular fa-moon"></i>
                    </strong>
                icons.
            </p>
        </div>
    </div>
</template>

<script>
import {ref} from "vue";
    
export default {
    data() {
        return {
            theme: "light",
        }
   
    },
    methods: {
        changeTheme () {
            this.theme = this.theme === "dark" ? "light" : "dark";
        }
    },
    setup () {
        const todo= ref("");
        const todos= ref([]);
        let theme= "light";

        const addTodo = () => {
            todos.value.push({
                done: false,
                content: todo.value,
                id: Date.now(),
            });
            todo.value= "";
        };
        const done = (todo) => {
            todo.done = !todo.done
        };
        const deleted = (todo) => {
            todo.content = ""
        };
        
        return {todo, todos, addTodo, done, deleted,};
    }
}
</script>

<style scoped>
.height100 {
    height: 100vh;
}
.done {
    text-decoration: line-through;
    cursor: pointer;
}
.pointer {
    cursor: pointer;
}
.floatRight {
    float: right;
}
.lightTheme {
    background-color: white;
}
.darkTheme {
    background-color: black;
    color: white;
}
</style>

