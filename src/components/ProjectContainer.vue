<template>
  <h2 class="project_container_title">Projects</h2>
  <p class="no_projects" v-if="projectList.length === 0">No projects yet</p>
  <div class="project_container">
    <Project
      v-for="project in projectList"
      :key="project.name"
      :project="project"
      :theme="project.theme"
    />
  </div>
</template>
<script>
import Project from "./Project.vue";

export default {
  props: ["projectList"],
  components: {
    Project,
  },
};
</script>
<style>
.project_container_title {
  margin-top: 30px;
}

.project_container {
  padding: 10px;
  max-width: 1000px;
  margin: 0 auto;
  font-weight: 500;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.no_projects {
  margin-top: 15px;
}
</style>
