<template>
  <div>
    <p>Completed Tasks: {{entries.filter(entry => {return entry.done === true}).length}}</p>
    <p>Pending Tasks: {{entries.filter(entry => {return entry.done === false}).length}}</p>
    <Entry
      v-for="(entry, index) in entries"
      v-bind:entry="entry"
      v-bind:index="index"
      :key="index"
      @delete-entry="deleteEntry"
      @complete-entry="completeEntry"
    ></Entry>
  </div>
</template>

<script type = "text/javascript" >
import Swal from 'sweetalert2'
import Entry from './Entry'
export default {
  props: ['entries'],
  components: {
    Entry
  },
  methods: {
    deleteEntry(entry) {
      Swal.fire({
        title: 'Are you sure?',
        text: 'This To-Do will be permanently deleted!',
        icon: 'warning',
        showCancelButton: true,
        confirmButtonColor: '#DD6B55',
        confirmButtonText: 'Yes, delete it!'
      }).then(result => {
        if (result.value) {
          const entryIndex = this.entries.indexOf(entry)
          this.entries.splice(entryIndex, 1)
          Swal.fire('Deleted!', 'Your To-Do has been deleted.', 'success')
        }
      })
      // if (reason == undefined) {
      // }
    },
    completeEntry(entry) {
      const entryIndex = this.entries.indexOf(entry)
      this.entries[entryIndex].done = true
    }
  }
}
</script>
<style>
</style>
