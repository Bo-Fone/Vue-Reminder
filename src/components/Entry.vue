  <template>
  <div class="ui centered card">
    <div class="content" v-show="!isEditing">
      <div class="header">{{ entry.title }}</div>
      <div class="meta">{{ entry.project }}</div>
      <div class="extra content">
        <span class="right floated edit icon" v-on:click="showForm">
          <i class="edit icon"></i>
        </span>
        <span class="right floated trash icon" v-on:click="deleteEntry(entry)">
          <i class="trash icon"></i>
        </span>
      </div>
    </div>
    <div class="content" v-show="isEditing">
      <div class="ui form">
        <div class="field">
          <label>Title</label>
          <input type="text" v-model="entry.title" />
        </div>
        <div class="field">
          <label>Project</label>
          <input type="text" v-model="entry.project" />
        </div>
        <div class="ui two button attached buttons">
          <button class="ui basic blue button" v-on:click="hideForm">Close X</button>
        </div>
      </div>
    </div>
    <div
      class="ui bottom attached green basic button"
      v-show="!isEditing &&entry.done"
      disabled
    >Completed</div>
    <div
      class="ui bottom attached red basic button"
      v-show="!isEditing && !entry.done"
      @click="completeEntry(entry)"
    >Pending</div>
  </div>
</template>

<script>
export default {
  props: ['entry'],
  data() {
    return {
      isEditing: false
    }
  },
  methods: {
    showForm() {
      this.isEditing = true
    },
    hideForm() {
      this.isEditing = false
    },
    deleteEntry(entry) {
      this.$emit('delete-entry', entry)
    },
    completeEntry(entry) {
      this.$emit('complete-entry', entry)
    }
  }
}
</script>
