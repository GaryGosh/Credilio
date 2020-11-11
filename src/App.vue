<template>
  <div id="app">
    <div class="container bg-red-500 h-64">
      <h1>#todo</h1>
      <input class="input" v-on:keypress.enter="add()" v-model="newTodo" />
      <button class="add-btn" v-on:click="add()">Add</button>
      <ul style="list-style-type: none;">
        <li v-for="(todo, index, isCompleted) in existingTodo">
          <input @change="taskUpdate(this)" :id="todo.id" v-model="todo.isCompleted" type="checkbox" class="form-checkbox bg-blue-900">
          <span class="todo.isCompleted?' line-through':''">
             {{todo.text}}
          </span>
          <button class="delete-button" @click="deleteTodo(index)">x</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      newTodo: "",
      existingTodo: [
        { text: "Get groceries", id: 0, isCompleted: false },
        { text: "Run errands", id: 1, isCompleted: true },
        { text: "Walk dog", id: 2, isCompleted: false }
      ]
    };
  },
  methods:{
    add(){
      this.existingTodo.push({
        text: this.newTodo,
        id: new Date().valueOf()
      }),
      this.newTodo = ''
    },
    deleteTodo(index){
      this.existingTodo.splice(index, 1)
    },
    taskUpdate(){
      this.existingTodo.forEach((key, item) => {
        if(item.id === this.$refs.id) {
          this.existingTodo.isCompleted = !this.existingTodo.isCompleted
          console.log(this.existingTodo);
        }
      })
      
    }
  }
};
</script>


