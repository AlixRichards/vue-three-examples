<template>
    <div>
        <h2>List of todos</h2>
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
        <p>{{completedToDos.length}} out {{ toDos.length }} items complete</p>
        <p>{{completedToDos}}</p>
    </div>
</template>

<script>
export default {
    name: 'ToDoList',
    data() {
        return {
            toDos: [],
            completedToDos: [],
        }
    },
    methods: {
        handleToDo(event) {
            // push the value to the array
            this.toDos.push(event.target.value);
            // clear the input
            event.target.value = '';
        },
        handleDelete(event) {
            // find label & get value
            const toDoValue = event.target.closest('li').querySelector('label').innerText;

            // loop through array to find index
            const arrayIndex = this.toDos.findIndex( item => item === toDoValue);

            // remove matching index from array
            this.toDos.splice(arrayIndex, 1) 

            // completed count
            const completedArrayIndex = this.completedToDos.findIndex( item => item === toDoValue);

            this.completedToDos.splice(completedArrayIndex, 1);
        }
    }
}
</script>