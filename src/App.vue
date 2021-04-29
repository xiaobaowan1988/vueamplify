<template>
  <div id="app">
    <amplify-authenticator>
      <div>
          <form v-on:submit.prevent>
            <button @click="createTodo">createTodo</button>
            <button @click="getTodos">getTodos</button>
            <button @click="deleteTodos">deleteTodos</button>
          </form>
        <amplify-sign-out></amplify-sign-out>
      </div>
    </amplify-authenticator>
  </div>
</template>

<script>
import { DataStore, Predicates } from '@aws-amplify/datastore';
// //import { createTodo } from './graphql/mutations';
// //import { listTodos } from './graphql/queries';
// import { onCreateTodo } from './graphql/subscriptions';
import {Todo} from './models';
 //import { AuthState, onAuthUIStateChange } from '@aws-amplify/ui-components'

export default {
  name: 'app',
  methods: {
   async createTodo(){
     const todo = await DataStore.save(new Todo({name:"a",description:"bb"}))
     console.log(todo)
    },
   async getTodos(){
     const todos = await DataStore.query(Todo)
     console.log("todos get successfully",JSON.stringify(todos, null, 2))
   },
   async deleteTodos(){
     await DataStore.delete(Todo,Predicates.ALL)
     console.log("todos delete successfully")
   }   
  }
}


</script>