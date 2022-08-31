<script setup>
import { ref , onMounted , computed , watch } from "vue";
import Addtodo from './components/addtodo.vue';



const name = ref('')
const todos = ref([])
const isopen = ref(false)

const del = (val)=>{
  todos.value.pop(val)
  localStorage.setItem('todos',JSON.stringify(todos.value))
}

watch(todos,(newVal)=>{
  localStorage.setItem('todos',newVal)
})


watch(name,(newVal)=>{
  localStorage.setItem('name',newVal)
})


onMounted(()=>{
  name.value = localStorage.getItem('name') || '',
  todos.value = JSON.parse(localStorage.getItem('todos')) || []
})


</script>

<template>
  <main>
    <img src="./assets/img/logo.png" alt="logo">
    <section class="first">
      <div class="name">
        Hello <input type="text" placeholder="name here" v-model="name">
      </div>
      <div class="logo">
        <img src="./assets/img/logo.png" alt="logo">
        <div>
          <h2>do it!</h2>
          <h3>your favorite APP :)</h3>
        </div>
      </div>
    </section>

    <section class="second">
      <div class="name">
        Hello , <input type="text" placeholder="name here" v-model="name">
      </div>
      <div class="top">
        <div class="text">my tasks</div>
        <button @click="isopen = true">+</button>
      </div>
      <div  v-for="todo in todos">
        <div class="item">
        <div class="left">
          <div class="title">{{todo.title}}</div>
          <div class="text">{{todo.desc}}</div>
        </div>
        <button @click="del(todo)"><img src="./assets/img/Group.png" alt=""></button>
       </div>
      </div>
      
    </section>
  </main>
  <Addtodo :isopen="isopen" @toggle="(value) => isopen = value"/>


</template>


