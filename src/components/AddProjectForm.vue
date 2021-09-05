<template>
  <div v-if="showAddProjectForm" class="add_project_form_container">
    <h3>Create a New Project</h3>
    <form action="none" autocomplete="off">
      <div class="form_field">
        <label for="project_name">Project Name:</label>
        <input ref="name" type="text" name="project_name" />
      </div>
      <div class="form_field">
        <label for="project_color">Project Color:</label>
        <select ref="color" name="project_color" id="project_color">
          <option value="blue">Blue</option>
          <option value="red">Red</option>
          <option value="green">Green</option>
          <option value="orange">Orange</option>
          <option value="yellow">Yellow</option>
        </select>
      </div>
      <button
        class="btn add_project_form_button"
        type="button"
        @click="addProject(this.$refs.name.value, this.$refs.color.value)"
      >
        Create Project
      </button>
    </form>
  </div>
</template>
<script>
export default {
  props: ["showAddProjectForm"],
  methods: {
    addProject(name, color) {
      if (name === "") return;
      this.$emit("addProject", name, color);
      this.$refs.name.value = "";
      this.$emit("closeForm");
    },
  },
};
</script>
<style>
.add_project_form_container {
  margin: 30px auto 0;
  padding: 20px 0px;
  max-width: 600px;
  border-radius: 10px;
  box-shadow: rgba(100, 100, 111, 0.2) 0px 7px 29px 0px;
}

.form_field {
  margin-top: 15px;
}

.form_field input,
.form_field select {
  margin-left: 10px;
  padding: 3px 5px;
}

.add_project_form_button {
  margin-top: 20px;
}
</style>
