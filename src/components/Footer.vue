<template>
    <footer>
        <div class="all">
            <input type="checkbox" id='footer' :checked="total!==0&&total===completed?true:false" @change="changeAllChecked($event.target.checked)">
            <label for="footer">Completed {{completed}}/ Total {{total}} </label>
        </div>
        <button @click='removeAll'>Delete all completions</button>
    </footer>
</template>

<script>
import {defineComponent} from 'vue'
export default defineComponent({
    name:'Footer',
    props:['todos','changeAllChecked','removeAll'],
    computed:{
        total(){
            return this.todos.length
        },
        completed(){
            return this.todos.reduce((preValue,value)=>{
                return preValue+(value.done?1:0)
            },0)
        }
    }
})
</script>

<style scoped>
    /* footer區域*/
    section footer{
        width: 100%;
        display: flex;
        justify-content: space-between;
        align-items: center;
    }
    section footer .all{
        flex: 1;
        padding: 0 0.5rem;
        display: flex;
        justify-content: flex-start;
        align-items: center;
        font-family:'Noto Sans', sans-serif; ; ;
    }
    section footer .all input+label{
        margin-left: 0.5rem;
    }
    section footer button{
        flex: 1;
        font-size: 16px;
        line-height: 24px;
        font-family: 'Noto Sans', sans-serif; ;
        cursor: pointer;
        border: none;
        padding: 0.3rem 0;
        border-radius: 0.5rem;
        background-color: rgb(223, 13, 94);
    }
    section footer button:hover{
        box-shadow: 0 0.2rem 0.2rem #555;
        color:#fff;
    }
</style>