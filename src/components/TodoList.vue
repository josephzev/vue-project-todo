<template>
	
	<div class="todo-list">

      <div class="row">

         <div class="columns large-4">

            <h2>Uncompleted ({{uncompletedTodos.length}})</h2>
    
            <todo v-for="todo in uncompletedTodos" v-bind:todo="todo" v-bind:key="todo.id" @delete-todo="deleteTodo(todo)" @toggle-todo="toggleTodo(todo)"></todo>

         </div>

         <div class="columns large-4">

            <h2>Completed ({{completedTodos.length}})</h2>
    
            <todo v-for="todo in completedTodos" v-bind:todo="todo" v-bind:key="todo.id" @delete-todo="deleteTodo(todo)" @toggle-todo="toggleTodo(todo)"></todo>

         </div>

        </div>

	</div>

</template>



<script type="text/javascript">

   import axios from 'axios';

   import todo from './todo';

   export default{

   	  name: 'TodoList',

        props: ['todos'],

        components: {

          todo

        },

        computed: {

         completedTodos: function(){

            return this.todos.filter(function(todo){

               return todo.status == 1;
            });
         },

         uncompletedTodos: function(){

            return this.todos.filter(function(todo){

               return todo.status == 0;
            });
         }
        },

        methods: {

          deleteTodo: function(todo){

              var todoIndex = this.todos.indexOf(todo);

              this.todos.splice(todoIndex, 1);

              axios.post('http://localhost/api/delete-todo', todo);
          },

          toggleTodo: function(todo){

              if(todo.status == 1){

                  todo.status = 0;

              }else{

               todo.status = 1;
              }

              axios.post('http://localhost/api/toggle-todo', todo);
              
          }

        }

   }
	
</script>



<style type="text/css">

    .todo-list{
      margin-left: auto;
      margin-right: auto;
    }
	
</style>