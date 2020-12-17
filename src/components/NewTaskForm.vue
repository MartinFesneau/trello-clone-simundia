<template>
  <div class="row">
      <div class="col form-inline">
        <input
          v-model="newTask"
          placeholder="enter new task"
          @keyup.enter="addTask"
          @submit.prevent="addTask"
        />
        <button class="btn btn-primary" @click="addTask">New task</button>
      </div>
    </div>
</template>

<script>
export default {
  emit: ['new-task'],
  data() {
    return {
      newTask: ''
    }
  },
  methods: {
    addTask() {
      if (this.newTask) {
        this.$emit('new-task', this.newTask );
        this.newTask = '';
      }
    },
  }
}
</script>

<style>

</style>