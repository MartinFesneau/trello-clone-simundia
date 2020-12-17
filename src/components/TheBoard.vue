<template>
  <new-task-form @new-task="add"></new-task-form>

  <div class="parent">
    <div class="todo">
      <h3>To Do</h3>
      <vue-draggable-next class="trello-col" :list="arrTodo" group="tasks">
        <task-item v-for="element in arrTodo"
          :key="element.id"
          :name="element.name"
          :status="element.status"
          :date="element.date">
        </task-item>
      </vue-draggable-next>
    </div>

    <div class="in-progress">
      <h3>In Progress</h3>
      <vue-draggable-next
        class="trello-col"
        :list="arrInprogress"
        group="tasks"
      >
        <task-item v-for="element in arrInprogress"
          :key="element.id"
          :name="element.name"
          :status="element.status">
        </task-item>
      </vue-draggable-next>
    </div>

    <div class="done">
      <h3>Done</h3>
      <vue-draggable-next class="trello-col" :list="arrDone" group="tasks">
        <task-item v-for="element in arrDone"
          :key="element.id"
          :name="element.name"
          :status="element.status">
        </task-item>
      </vue-draggable-next>
    </div>
  </div>
</template>

<script>
import { VueDraggableNext } from "vue-draggable-next";
import NewTaskForm from './NewTaskForm';
import TaskItem from './TaskItem'

export default {
  components: {
    NewTaskForm,
    VueDraggableNext,
    TaskItem
  },
  data() {
    return {
      arrTodo: [],
      arrInprogress: [],
      arrDone: [],
    };
  },
  methods: {
    async add(newTask) {
      console.log(newTask);
      this.arrTodo.push( {name: newTask});

      const task = { task: { name: newTask }};

      await fetch(`http://localhost:3000/tasks`, {
        method: "POST",
        headers: {
        "Content-Type": "application/json"
        },
        body: JSON.stringify(task)
        });
    },
    async loadTasks() {
      const response = await fetch("http://localhost:3000/tasks");
      const responseData = await response.json();
      console.log(responseData)
      responseData.forEach((key) => {
        const task = {
          date: new Date(key.created_at),
          id: key.id,
          name: key.name,
          status: key.status,
        };
        this.arrTodo.push(task);
      });
    },
    deleteTask(e) {
      console.log(e)
    }
  },
  created() {
    this.loadTasks();
  }
};
</script>

<style scoped>
.parent {
  margin: 0 auto;
  display: grid;
  justify-items: center;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: 1fr;
  grid-column-gap: 32px;
  grid-row-gap: 0px;
}
.trello-col {
  min-height: 300px;
  display: flex;
  flex-direction: column;
  padding: 25px;
  background-color: white;
  width: 256px;
}

.todo {
}
</style>
