<template>
  <div id="app">
    <img src="./assets/logo.png" />
    <Reminder v-bind:entries="entries" />
    <CreateEntry v-on:create-entry="createEntry" />
  </div>
</template>

<script>
import Swal from 'sweetalert2'
import Reminder from './components/Reminder'
import CreateEntry from './components/CreateEntry'

export default {
  name: 'App',
  components: {
    Reminder,
    CreateEntry
  },
  data() {
    return {
      entries: [
        {
          title: 'Todo A',
          project: 'Project A',
          done: false
        },
        {
          title: 'Todo B',
          project: 'Project B',
          done: true
        },
        {
          title: 'Todo C',
          project: 'Project C',
          done: false
        },
        {
          title: 'Todo D',
          project: 'Project D',
          done: false
        }
      ]
    }
  },
  methods: {
    createEntry(entry) {
      this.entries.push(entry)
      Swal.fire('Success!', 'To-Do created!', 'success')
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
