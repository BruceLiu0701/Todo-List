<template>
    <div class="input">
        <input type="text" placeholder="Plaese enter your todo here !" v-model="whatTodo">
        <div class="yourTime">
            <input type="date" v-model="whatDate">
            <input type="time" v-model="whatTime">
        </div>
        <button @click="addNewTodo">Add to list</button>
    </div>
</template>

<script>
import {defineComponent} from 'vue'
import Swal from 'sweetalert2'
import {nanoid} from 'nanoid'
export default defineComponent({
    name:'UserInput', 
    props:['getData'],   // 接收到放在props的函式被放在UserInput的實體物件vc上了,可以在函式內直接透過this使用或是表達式內直接使用
    data() {
        return {
            whatTodo:'',
            whatDate:'',
            whatTime:''
        }
    },
    methods:{
        addNewTodo(){
            if(this.whatTodo.trim()!==''&& this.whatDate.trim()!==''&& this.whatTime.trim()!==''){
                const newObj={id:nanoid(),title:this.whatTodo,date:this.whatDate,time:this.whatTime,done:false}
                this.getData(newObj)
                this.whatTodo='';
                this.whatDate='';
                this.whatTime='';
                return
            }
            Swal.fire({
                icon: 'error',
                title:'輸入不能為空',
                text: '請確認代辦事項、日期、時間是否已完成輸入',
            })
        }
    }
})
</script>

<style scoped>
    /* 輸入區域 */
    section .input{
        width: 100%;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        margin-bottom: 1.5rem;
    }
    section .input input{
        width: 100%;
        padding: 0.6rem 0;
        font-size: 16px;
        text-indent: 0.5rem;
        margin-bottom: 0.5rem;
        border: 2px solid rgb(236, 9, 168);
    }
    section .input input:focus{
        outline: none;
        box-shadow: 0 0 0.5rem rgb(223, 13, 160);
    }
    section .input input::placeholder{
        color:rgb(210, 111, 223);
    }
    section .input .yourTime{
        width: 100%;
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 0.5rem;
    }
    section .input .yourTime input{
        width: 100%;
        height: 2rem;
        margin-bottom:0 ;
    }
    section .input .yourTime input+input{
        margin-left: 0.5rem;
    }
    section .input button{
        font-size: 16px;
        line-height: 24px;
        font-family: 'Noto Sans', sans-serif; ;
        cursor: pointer;
        width: 100%;
        border: none;
        padding: 0.3rem 0;
        border-radius: 0.5rem;
        background-color: rgb(223, 13, 94);
    }
    section .input button:hover{
        box-shadow: 0 0.2rem 0.2rem #555;
        color:#fff;
    }
</style>