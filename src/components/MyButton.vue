 <template>
<button
    v-bind:style="{background: backgroundInterno, color: colorInterno}"
    :disabled="disableInterno"
    @click="consoleVer"
>
Button
</button>

 </template>

 <script lang="ts">
 import { defineComponent } from 'vue'
 
 export default defineComponent({
    name: "MyButton",
    data (){
        return{
        }
    },
    props: {
        backgroundInterno: {
            type: String
        },
        colorInterno : {
            type: String
        },
      disableInterno: {
            type: Boolean 
        }
    },
    methods:{
        consoleVer(e : any){
            return console.log(this.colorInterno, 1)
        }
    }
        
 });
 </script>

 <style scoped>
button {
  border: none;
  padding: 10px 40px;
  border-radius: 5px;
  font-size: 16px;
  cursor: pointer;
}
button:disabled {
  opacity: 0.5;
}
button:hover {
  filter: brightness(125%);
}
 </style>
 