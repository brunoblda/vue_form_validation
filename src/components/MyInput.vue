<template>
    <div class="label">
        <label :for="name">{{name}}</label>
        <div class="error">{{error}}</div>
    </div>
    <input  
        :id="name"
        :value="valor_user" 
        :type="type"
        @input="inputF"
    />

    <!--  
        v-model="valor"
    -->

    <!-- 

        :value="valor"
        @input="input"

    -->
    
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
name: "MyInput",
data (){
    return{
        valor: '',
        objectIup: {
            n1: '',
            n2: ''
        }
    }

},
props: {
    type: {
        type: String,
        default: 'text'
    },
    name:{
        type: String,
        required: true

    },
    id_input:{
        type: Number,
        required: true
    },
    rules: {
        //required: boolean
        //min: number
        type: Object,
        default: () => ({})
        
    },
    valor_user: {
        type: String,
        required: true
    },
    error: {
        type: String
    } 
},
created(){
    this.$emit('update', {
        id: this.id_input,
        valor_campo: this.valor_user,
        error: this.validate(this.valor_user)
    } )

},emits:['update'],
methods:{
    input($event: any){
        this.valor = $event.target.value
    },
    inputF($event: any){
        this.$emit('update', {
            id: this.id_input,
            valor_campo: $event.target.value,
            error: this.validate($event.target.value)
        } )
    },
    validate(valor_input: string){
        if(this.rules.required && valor_input.length === 0){
            return 'Valor é requerido'
        }
        if(this.rules.min && valor_input.length < this.rules.min ){
            return `O tamanho mínimo é ${this.rules.min}`
        }
        else{
            return ''
        }

    }

},
computed:{
}
    
});
</script>

<style scoped>
    .input_wrapper{
        display: flex;
        flex-direction: column;
    }
    .error {
        color: red;
    }
    .label{
        display: flex;
        justify-content:flex-start; 
    }
    input{
        border: 1px solid silver;
        border-radius: 5px;
        padding: 10px;
        margin: 5px 0;
        font-size: 16px;

    }
</style>
 