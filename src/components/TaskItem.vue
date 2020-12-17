<template>
  <div class="task-item">
    <span>{{ name }}</span><span>{{ status }}</span>
    <time>{{ date }}</time>
  </div>
</template>

<script>
export default {
  props: ['name', 'status', 'date']
};
</script>

<style scoped>
.task-item {
  border: 1px solid lightblue;
  border-radius: 5px;
  margin: 16px;
  /* padding: 16px; */
  background-color: white;
}
</style>
