<template>
  <div>
    <h3>My TODO</h3>
    <input v-model="newTodo" placeholder="Input here...">
    <button v-on:click="addTodo()">追加</button>
    <h5>ToDo List</h5>
    <ul>
      <li v-for="(todo, i) in todos" v-bind:key="i">
        {{ todo }}
        <button v-on:click="deleteTodo(todos.id)">削除</button>
        <button v-on:click="PutTodo(todos)">編集</button>
      </li>
    </ul>    
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      todos: [],
      newTodo: ""
    }
  },
  created(){
        axios.get('http://localhost:3000/todos')
            .then(response => this.todos = response.data)
            .catch(error => console.log(error))
    },
  methods: {
    addTodo: function() {
      axios.post('http://localhost:3000/todos',{newTodo: this.newTodo})
        .then(response => this.newTodo.push(response))
        .catch(error => console.log(error))    
    },
    deleteTodo: function() {
      axios.delete('http://localhost:3000/todos/', {data: this.todos.id} )
      .then(response => (response.data))
      .catch(error => console.log(error))       
    },
    PutTodo: function(){
      axios.put('http://localhost:3000/todos/' , {id: this.todos.Number} )
      .then(response => (response.data))
      .catch(error => console.log(error))  
    }
  }
}
</script>