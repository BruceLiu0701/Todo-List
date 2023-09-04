<template>
    <header>
        <h2>Todo List</h2>
        <p>What will you do ?</p>
    </header>
</template>

<script>
import {defineComponent} from 'vue'
export default defineComponent({
    name:'Header',
})
</script>

<style scoped>
    section header{
        width: 100%;
        margin-bottom: 1rem;
        text-align: center;
        font-family: 'Noto Sans', sans-serif;
    }
    section header h2{
        font-size: 40px;
        line-height: 52px;
        margin-bottom: 1rem;
    }
    section header p{
        font-size: 16px;
        line-height: 24px;
    }
</style>