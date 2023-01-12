<template>
  <div>
    <h1>Hello World</h1>
    <ul>
      <li
        v-for="(todoElem, ind) in todoList"
        :key="ind"
      >
        {{ todoElem.text }}
      </li>
    </ul>
    <form @submit="formSubmit">
      <input type="text" name="newTodo" v-model="newTodo">
      <input type="submit" value="CREATE">
    </form>
  </div>
</template>

<script>

import axios from 'axios';

const API_URL = "http://localhost/php-todo-list-json/phpApi/api.php";

export default {
  name: 'JsonTest',
  data() {

    return {

      newTodo: "",

      todoList: []
    };
  },
  methods: {

    formSubmit(e) {

      e.preventDefault();
      
      const params = { params: { 
        'newTodo': this.newTodo
      }};

      axios.get(API_URL + "api-create-todo.php", params)
           .then(() => {

             this.getAllData();
           });
    },
    getAllData() {

      axios.get(API_URL + "api.php")
         .then(res => {

            const data = res.data;

            this.todoList = data;
         });
    }
  },
  mounted() {

    this.getAllData();
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>