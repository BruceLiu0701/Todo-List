
<template>
    <section>
        <Header/>
        <UserInput :getData="getData"/>
        <List :todos="todos" :changeChecked="changeChecked" :deleteTodo='deleteTodo' :handleEdit="handleEdit" :editTodo="editTodo"/>
        <Footer :todos="todos" :changeAllChecked="changeAllChecked" :removeAll='removeAll'/>
    </section>
</template>

<script>
  import {defineComponent} from 'vue'
  import Swal from 'sweetalert2'
  import Header from './components/Header.vue'
  import UserInput from './components/UserInput.vue'
  import List from './components/List.vue'
  import Footer from './components/Footer.vue'
  export default defineComponent({
    name:'App',
    // 註冊組件
    components:{
      Header,
      UserInput,
      List,
      Footer
    },
    data() {
        return {
            todos:[
                {id:'001',title:'吃口飯',date:'2023-08-03',time:'11:30',done:true,edit:false},
                {id:'002',title:'睡個覺',date:'2023-09-04',time:'22:00',done:false,edit:false},
                {id:'003',title:'寫code',date:'2023-10-05',time:'09:30',done:false,edit:false}
            ],
        }
    },
    methods:{
      // 添加新代辦到陣列中的函式
      getData(newObj){
        this.todos.unshift(newObj)   // Vue能捕獲到使用unshift陣列方法引起的數據改變, React中不要使用這種寫法
      },
      // 更改勾選狀態的函式
      changeChecked(done,id){
        const newObj=this.todos.map((value)=>{
            if(value.id===id) return {...value,done}
            else return value
        })
        this.todos=newObj
      },
      // 刪除todo的函式
      deleteTodo(id){
        Swal.fire({
            title: '確定要刪除此事項嗎?',
            icon: 'warning',
            showCancelButton: true,
            confirmButtonColor: '#3085d6',
            cancelButtonColor: '#d33',
            confirmButtonText: '確認',
            cancelButtonText: '取消'
          }).then((result) => {
            if (result.isConfirmed) {
              Swal.fire(
                '刪除成功!',
                '',
                'success'
              )
              const newObj=this.todos.filter((value)=>{
                return value.id!==id
              })
              this.todos=newObj
            }
        })  
      },
      // 改變全部done的函式
      changeAllChecked(done){
        const newObj=this.todos.map((value)=>{
          return {...value,done}
        })
        this.todos=newObj
      },
      // 處理是否為可編輯狀態的函式
      handleEdit(id){
        const newObj=this.todos.map((value)=>{
            if(value.id===id) return {...value,edit:!value.edit}
            else return value
        })
        this.todos=newObj
      },
      // 修改todo事項的函式
      editTodo(title,id){
        const newObj=this.todos.map((value)=>{
            if(value.id===id) return {...value,title}
            else return value
        })
        this.todos=newObj
      },
      // 刪除全部已完成todo的函式
      removeAll(){
        const total=this.todos.reduce((preValue,value)=>{
            return preValue+(value.done?1:0)
        },0)
        if(total!==0){
          Swal.fire({
            title: '確定要刪除已完成事項嗎?',
            icon: 'warning',
            showCancelButton: true,
            confirmButtonColor: '#3085d6',
            cancelButtonColor: '#d33',
            confirmButtonText: '確認',
            cancelButtonText: '取消'
          }).then((result) => {
            if (result.isConfirmed) {
              Swal.fire(
                '刪除成功!',
                '',
                'success'
              )
              const newObj=this.todos.filter((value)=>{
                return !value.done
              })
              this.todos=newObj
            }
          })
        }else{
          Swal.fire({
              icon: 'error',
              title:'沒有已完成事項',
              text: '',
          })
        }
      }
    }
  })
</script>

<style>
  section{
    width: 460px;
    border-radius: 2rem;
    padding: 2.5rem ;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    box-shadow: 0 0 50px rgb(144, 215, 233);
    background:linear-gradient(180deg,rgb(210, 111, 223),rgb(219, 87, 142));
}
</style>
