<template>
    <ul>
        <li v-for="value in todos" :key="value.id">
            <div class="item">
                <div class="willDo">
                    <input 
                    type="checkbox" 
                    :id='value.id' 
                    :checked='value.done' 
                    @change="changeChecked($event.target.checked,value.id)">
                    <label :for='value.id' v-show="!value.edit" >{{value.title}}</label>
                    <input type='text' 
                    v-show="value.edit"  
                    :value="value.title" 
                    @blur="handleEdit(value.id)" 
                    @input="editTodo($event.target.value,value.id)">
                </div>
                <p>{{value.date}} {{value.time}}</p>
            </div>
            <div class="modify">
                <span class="material-symbols-outlined" @click="handleEdit(value.id)">edit_note</span>
                <span class="material-symbols-outlined" @click='deleteTodo(value.id)'>delete</span>
            </div>
        </li>
    </ul>
</template>

<script>
import {defineComponent} from 'vue'
export default defineComponent({
    name:'List',
    // 接收到props的函式被放在UserInput的實體物件vc上了,可以在函式內直接透過this使用或是"表達式內直接使用"
    props:['todos','changeChecked','deleteTodo','handleEdit','editTodo'], 
    methods:{
        amend(){
            this.modify= !this.modify
        },
    }
})
</script>

<style scoped>
    /* list區域*/
    section ul{
        width: 100%;
        margin-bottom: 1.5rem;
    }
    section ul li{
        border: 2px solid #eca713;
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 0.5rem;
    }
    section ul li+li{
        margin-top: 0.2rem;
    }
    section ul li .item{
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: flex-start;
        font-family: 'Noto Sans', sans-serif;
        font-size: 16px;
        line-height: 24px;
    }
    section ul li .item p{
        width: 100%;
        padding-left: 1.5rem;
        color: rgb(135, 14, 151);
    }
    section ul li .item input:last-of-type{
        margin-left:0.5rem;
    }
    section ul li .item .willDo{
        display:flex;
        justify-content:flex-start;
        align-items:center;
    }
    section ul li .item .willDo label{
        padding-left:0.5rem;
    }
    section ul li .item .willDo input+p{
        font-size: 16px;
        font-weight: bold;
        color: #000;
    }
    /* list 右方修改刪除區域*/
    section ul li .modify{
        display: none;
        color:rgb(223, 13, 94);
    }
    section ul li .modify span{
        cursor: pointer;
        font-size:30px;
    }
    section ul li .modify span:hover{
        color:rgb(97, 9, 109);
    }    
    section ul li:hover{
        background-color: #e491dd;
    }
    section ul li:hover .modify{
        display: block;
    }
</style>