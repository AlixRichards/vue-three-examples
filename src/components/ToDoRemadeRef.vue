<template>
    <div>
        <h2>{{title}}</h2>
        <input 
            @keyup.enter="handleToDo"
        />
        <label></label>
        <ul>
            <li v-for="(item, index) in toDos" :key="index">
                <input type="checkbox" :id="`checkbox--${index}`" :value="`${item}`" v-model="completedToDos">
                <label :for="`checkbox--${index}`">{{item}}</label>
                <button @click="handleDelete">delete</button>
            </li>
        </ul>
        <p v-if="toDos.length">{{completedToDos.length}} out {{ toDos.length }} items complete</p>
        <p v-if="completedToDos.length">{{completedToDos}}</p>
    </div>
</template>

<script>
import { reactive, onMounted, ref } from 'vue';
export default {
    name: 'ToDoRemade',
    props: {
        title: {
            type: String,
            default: 'My List of ToDos'
        }
    },
    setup(props) {
        const toDos = ref([]);
        const completedToDos = ref([]);

        function handleToDo(event) {
            // push the value to the array
            toDos.value.push(event.target.value);
            // clear the input
            event.target.value = '';
        }

        function handleDelete(event) {
            // find label & get value
            const toDoValue = event.target.closest('li').querySelector('label').innerText;

            // loop through array to find index
            const arrayIndex = toDos.value.findIndex( item => item === toDoValue);

            // remove matching index from array
            toDos.value.splice(arrayIndex, 1) 

            // completed count
            const completedArrayIndex = completedToDos.value.findIndex( item => item === toDoValue);

            completedToDos.value.splice(completedArrayIndex, 1);
        }

        onMounted( () => {
            console.log(props.title);
        })

        return {
            toDos,
            completedToDos,
            handleToDo,
            handleDelete,
        }
    },
}
</script>