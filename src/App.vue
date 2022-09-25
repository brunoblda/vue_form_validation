<template>
  <form @submit.prevent="submit">
    <my-input 
      name="Username"
      :id_input="username.id" 
      :rules="{required: true, min: 5}"
      :valor_user="username.value"
      :error="username.error"
      @update="updateIn"
      />
    <my-input 
      name="Password"
      :id_input="password.id"
      :rules="{required: true, min: 10}"
      :valor_user="password.value"
      :error="password.error"
      type="password"
      @update="updateIn"
      />
    <HelloWorld />
    <myButton
      backgroundInterno='darkslateblue'
      colorInterno='white'
      :disableInterno='!valid'
    />
  </form>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import HelloWorld from './components/HelloWorld.vue';
import MyButton from './components/MyButton.vue';
import MyInput from './components/MyInput.vue';

export default defineComponent({
  name: 'App',
  components: {
    HelloWorld,
    MyButton,
    MyInput
  },
  data(){
    return{
      username:{
        id: 0,
        value:'User',
        error: ''
      }, 
      password:{
        id: 1,
        value:'pass',
        error: ''
      }, 
    }
  },

  methods:{
    updateIn({id, valor_campo, error}: any){
      if (this.username.id === id){
        this.username.value = valor_campo
        this.username.error = error
      }
      if (this.password.id === id){
        this.password.value = valor_campo
        this.password.error = error
      }
    },
    submit($event: any){
      console.log('Event')
    }
  },
  computed: {
    valid(): boolean{
      return (
        !this.username.error && 
        !this.password.error
      )
    }
  }
  
});
</script>

<style>
</style>
