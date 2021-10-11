<template>
	
	<div class="todo">

		<div class="row">

			<div class="column large-2">
				
				<button class="todo-complete-icon" :class="{completed: todo.status == 1}" @click="toggleTodo(todo)"></button>

			</div>

		    <div class="column large-10">

				<h3>{{ todo.title }}</h3>
		        <p> {{ todo.description }}</p>

		        <button class="button alert" v-on:click="deleteTodo(todo)">Delete</button>

           </div>

           <div class="column large-10">
           	
           	   <input type="text" placeholder="Enter title" v-model="todo.title"  ref="title">
           	   
                <textarea placeholder="Enter description" v-model="todo.description"  ref="project"></textarea>
                
                <button class="button success" v-on:click="updateTodo(todo.id, todo.title, todo.descripton, todo.status)">Update &amp; Close</button>

                <button class="button alert" v-on:click="closeForm">Cancel</button>

           </div>

       </div>

	</div>

</template>


<script>

    import axios from 'axios';
	
	export default{

		name: 'todo',

		props: ['todo'],

		methods: {

			deleteTodo: function(todo){

				this.$emit('delete-todo',todo);
			},

			toggleTodo: function(todo){

				this.$emit('toggle-todo',todo);
			},

			updateTodo: function(id, title, description, status){

				var data = {
					id: id,
					title: title,
					description: description,
					status: status
				}

				axios.post('http://localhost/api/update-todo', data);

			}
		}

	}
</script>

<style>

    .todo{
        padding: 20px;
        border: 1px solid #ccc;
        margin-bottom: 20px;
    }
    .todo-complete-icon{
        width: 30px;
        height: 30px;
        border: 2px solid #ccc;
        border-radius: 50%;
        margin-right: 40px;
        margin-top: 10px;
        position: relative;
        cursor: pointer;
    }
    .todo-complete-icon.completed{
        border-color: #00c996;
    }
    .todo-complete-icon.completed:before{
        content: "\2714";
        font-size: 36px;
        position: absolute;
        top:-10px;
        left:4px;
        color: #00c996;
    }

	
</style>