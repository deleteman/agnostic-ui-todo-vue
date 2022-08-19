<script setup>
import ToDoItem from "./ToDoItem.vue";
import {Divider, Card, Input, Button, Icon} from 'agnostic-vue'
</script>


<script>
export default {
    data() {
        return {
            todos: [],
            taskError: ""
        }
    },
    methods: {
        setTaskError(err) {
            this.taskError = err
        },
        setTodos(todos) {
            this.todos = todos
        },
        removeTodo(id) {
            this.setTodos(this.todos.filter( t => t.id != id))
        },
        addToDo(evt) {
            evt.preventDefault()
            console.log(evt)

            let input = evt.target.getElementsByTagName("input").item(0)
            let value = input.value
            
            if(value.trim() == "") {
                return this.setTaskError("Can't create empty task")
            } else {
                this.setTaskError("")
            }

            this.setTodos([...this.todos, {
                text: value,
                id: this.todos.length + 1
            }])
            input.value = ""
        },
        removeTodo(id) {
            this.setTodos(this.todos.filter( t => t.id != id))
        },
        isInputError() {
            return this.taskError.length != 0
        }
    }
}


</script>

   
<template>
        <section  id="main-section">
        <Card is-border is-shadow >
            <div class="w-100">
                <h1 class="p16">[Vue] Agnostic To-Do app</h1>
                <form @submit="this.addToDo"  class="p32">
                    <section class="p8">
                    <Input
                        id="standard-basic" 
                        label="New Task" 
                        type="text" 
                        :is-invalid="this.isInputError()"
                        :invalid-text="this.taskError"
                    />
                    </section>
                    <Button  type="submit" id="save-task-btn" >
                        Save task
                        <Icon>
                            <svg class="svg-icon" viewBox="0 0 20 20">
                                <path d="M17.064,4.656l-2.05-2.035C14.936,2.544,14.831,2.5,14.721,2.5H3.854c-0.229,0-0.417,0.188-0.417,0.417v14.167c0,0.229,0.188,0.417,0.417,0.417h12.917c0.229,0,0.416-0.188,0.416-0.417V4.952C17.188,4.84,17.144,4.733,17.064,4.656M6.354,3.333h7.917V10H6.354V3.333z M16.354,16.667H4.271V3.333h1.25v7.083c0,0.229,0.188,0.417,0.417,0.417h8.75c0.229,0,0.416-0.188,0.416-0.417V3.886l1.25,1.239V16.667z M13.402,4.688v3.958c0,0.229-0.186,0.417-0.417,0.417c-0.229,0-0.417-0.188-0.417-0.417V4.688c0-0.229,0.188-0.417,0.417-0.417C13.217,4.271,13.402,4.458,13.402,4.688"></path>
                            </svg>
                        </Icon>
                    </Button>
                </form>
                <Divider ></Divider>
                <div class="w-100 flex-column p16" >
                    <div v-for="todo in todos">
                     <ToDoItem :item="todo" :itemRemover="this.removeTodo" />
                    </div>
                </div>
                <Card >
                    <h2 class="p32">Total pending tasks: {{todos.length}}</h2>
                </Card>
            </div>
        </Card> 
        </section>
    
</template>

<style scoped>
#save-task-btn {
  float: right;
}

#main-section {
  width: 50%;
  margin: 0 auto;
}
</style>