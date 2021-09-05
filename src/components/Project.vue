<template>
  <div class="project_form_container">
    <div :class="theme" class="project">
      <div class="project_headline">
        <h3>{{ project.name }}</h3>
        <button @click="toggleNewTaskForm">New Task</button>
      </div>
      <p class="date">{{ project.getDate() }}</p>
      <hr />
      <div class="task_stats">
        <button @click="toggleTaskList">
          {{ ViewOrHide }} <span>{{ project.getTaskLength() }}</span> Tasks
        </button>
        <p>
          Completed {{ project.getCompletedTasks() }} /
          {{ project.getTaskLength() }}
        </p>
      </div>
      <div v-show="showTaskList">
        <Task v-for="task in project.tasks" :task="task" :key="task" />
      </div>
    </div>
    <NewTaskForm
      v-if="showNewTaskForm"
      :project="project"
      @closeTaskForm="toggleNewTaskForm"
    />
  </div>
</template>
<script>
import NewTaskForm from "./NewTaskForm.vue";
import Task from "./Task.vue";

export default {
  props: ["project", "theme"],
  components: {
    NewTaskForm,
    Task,
  },
  data() {
    return { showNewTaskForm: false, showTaskList: false, ViewOrHide: "View" };
  },
  methods: {
    toggleNewTaskForm() {
      this.showNewTaskForm = !this.showNewTaskForm;
    },
    toggleTaskList() {
      this.showTaskList = !this.showTaskList;
      if (this.showTaskList === false) this.ViewOrHide = "View";
      else this.ViewOrHide = "Hide";
    },
  },
};
</script>
<style>
.project_form_container {
  display: flex;
  flex-direction: column;
  width: 300px;
  margin: 10px;
}

.project {
  width: 100%;
  padding: 15px 20px 8px;
  border-radius: 5px;
  text-align: left;
  margin-bottom: 10px;
}

.project_headline {
  display: grid;
  grid-template-columns: 2fr 1fr;
  align-content: center;
}

.project_headline h3 {
  font-size: 1rem;
  font-weight: 500;
  color: #2c3e50;
  text-transform: capitalize;
}

.task_stats {
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.task_stats p {
  font-size: 0.8rem;
  font-weight: 600;
  color: inherit;
}

.project button {
  align-self: start;
  justify-self: end;
  border: none;
  padding: 2px 3px;
  border-radius: 5px;
  font-size: 0.8rem;
  font-weight: 600;
  color: inherit;
  background-color: transparent;
  cursor: pointer;
  transition: background-color 0.4s;
}

.project button:hover {
  background-color: #f0f0f0;
}

.project button span {
  color: #2c3e50;
}

.date {
  padding: 5px 0px 10px;
  font-size: 0.8rem;
  font-weight: 500;
  color: #646464;
}

.project hr {
  border: none;
  height: 1px;
  margin-bottom: 10px;
  background-color: #d3d3d3;
}

/* Project theme selectors */
.blue {
  border: 2px solid #0d3b9b;
  color: #0d3b9b;
}

.red {
  border: 2px solid #9b0d0d;
  color: #9b0d0d;
}

.green {
  border: 2px solid #0d9b54;
  color: #0d9b54;
}

.yellow {
  border: 2px solid #c9c426;
  color: #c9c426;
}

.orange {
  border: 2px solid #e39f20;
  color: #e39f20;
}
</style>
