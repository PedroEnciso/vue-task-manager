<template>
  <div class="title">
    <h1>Task Manager</h1>
    <button @click="toggleForm" class="btn">Add a Project</button>
  </div>
  <p class="description">Manage all of your projects and tasks in one place!</p>
  <AddProjectForm
    :showAddProjectForm="showAddProjectForm"
    @addProject="addProject"
    @closeForm="toggleForm"
  />
  <ProjectContainer :projectList="projectList" />
</template>

<script>
import moment from "moment";
import ProjectContainer from "./components/ProjectContainer.vue";
import AddProjectForm from "./components/AddProjectForm.vue";

// constructor for a new project
const Project = (name, theme) => {
  const tasks = [];

  const getDate = () => {
    return moment().format("MMM DD");
  };

  const addTask = (task) => {
    tasks.push(task);
  };

  // returns the amount of tasks in task array
  const getTaskLength = () => {
    return tasks.length;
  };

  const getCompletedTasks = () => {
    let count = 0;
    for (let i = 0; i < tasks.length; i++) {
      if (tasks[i].isComplete() === true) count++;
    }
    return count;
  };
  return {
    name,
    theme,
    tasks,
    getDate,
    addTask,
    getTaskLength,
    getCompletedTasks,
  };
};

export default {
  name: "App",
  data() {
    return {
      showAddProjectForm: false,
      projectList: [],
    };
  },
  components: {
    ProjectContainer,
    AddProjectForm,
  },
  methods: {
    // show/hide Add Project form
    toggleForm() {
      this.showAddProjectForm = !this.showAddProjectForm;
    },
    // add a project projectList
    addProject(projectName, projectTheme) {
      const newProject = Project(projectName, projectTheme);
      this.projectList.push(newProject);
    },
  },
};
</script>

<style>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

body {
  padding: 0 1rem;
}

.btn {
  padding: 5px 10px;
  height: fit-content;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.title {
  display: flex;
  justify-content: space-between;
  align-items: center;
  max-width: 600px;
  margin: 60px auto 0px;
}

.description {
  margin-top: 20px;
}
</style>
