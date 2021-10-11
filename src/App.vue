<template>

  <div id="app">


    <h1>{{ reversedMessage }}</h1>

  </div>

</template>

<script>


  import axios from 'axios';
  
  import test from './components/test'

  export default {
    name: 'App',

    data: function(){

      return{

       message: 'hello world'
      }

    },

    computed: {

       reversedMessage(){
          return this.message.split('').reverse().join('')  
      }
    },

    mounted: function(){

    },

    methods: {

      
    }
}
</script>

<style>

   .is-loading{

     background-color: blue;
   }

</style>
