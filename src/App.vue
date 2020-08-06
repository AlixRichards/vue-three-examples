<template>
    <img alt="kittens" src="http://placekitten.com/500/300" />
    <ToDoRemadeRef title="Alix's cool list of things"/>
</template>

<script>
import ToDoRemadeRef from './components/ToDoRemadeRef.vue'

export default {
  name: 'App',
  components: {
      ToDoRemadeRef,
  }
}
</script>
