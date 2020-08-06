<template>
    <div>
        <h2>{{title}}</h2>
        <input 
            @keyup.enter="handleToDo"
        />
        <label></label>
        <ul>
            <li v-for="(item, index) in state.toDos" :key="index">
                <input type="checkbox" :id="`checkbox--${index}`" :value="`${item}`" v-model="state.completedToDos">
                <label :for="`checkbox--${index}`">{{item}}</label>
                <button @click="handleDelete">delete</button>
            </li>
        </ul>
        <p v-if="state.toDos.length">{{state.completedToDos.length}} out {{ state.toDos.length }} items complete</p>
        <p v-if="state.completedToDos.length">{{state.completedToDos}}</p>
    </div>
</template>

<script>
import { reactive, onMounted } from 'vue';
export default {
    name: 'ToDoRemade',
    props: {
        title: {
            type: String,
            default: 'My List of ToDos'
        }
    },
    setup(props) {
        const state = reactive({
            toDos: [],
            completedToDos: [],
        })

        function handleToDo(event) {
            // push the value to the array
            state.toDos.push(event.target.value);
            // clear the input
            event.target.value = '';
        }

        function handleDelete(event) {
            // find label & get value
            const toDoValue = event.target.closest('li').querySelector('label').innerText;

            // loop through array to find index
            const arrayIndex = state.toDos.findIndex( item => item === toDoValue);

            // remove matching index from array
            state.toDos.splice(arrayIndex, 1) 

            // completed count
            const completedArrayIndex = state.completedToDos.findIndex( item => item === toDoValue);

            state.completedToDos.splice(completedArrayIndex, 1);
        }

        onMounted( () => {
            console.log(props.title);
        })

        return {
            state,
            handleToDo,
            handleDelete,
        }
    },
}
</script>