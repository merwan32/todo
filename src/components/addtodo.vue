<script setup>
import { ref ,watch , onMounted} from "vue";
const props = defineProps({
    isopen : Boolean
});
const todos = ref([])
onMounted(()=>{
  todos.value = JSON.parse(localStorage.getItem('todos')) || []
})
const emit = defineEmits('toggle');

const input_title = ref('')
const input_desc = ref('')


const addtodo= () => {
    if (input_title.value.trim() !== '' && input_desc.value.trim() !== '' ){
        todos.value.push({
            title : input_title,
            desc : input_desc
        })
        localStorage.setItem('todos',JSON.stringify(todos.value)),
        emit('toggle',false),
        location.reload();
    }
}
watch(todos,(newVal)=>{
  localStorage.setItem('todos',newVal)
})


</script>

<template>
    <div class="form" v-if="props.isopen" >
        <div class="menu" >
            <img @click="emit('toggle',false)" src="../assets/img/close.png" alt="">
            <div class="title">add To Do</div>
            <input type="text" placeholder="type title here" v-model="input_title">
            <input type="text" placeholder="type description here" v-model="input_desc">
            <button @click="addtodo">Add</button>
        </div>
    </div>
</template>