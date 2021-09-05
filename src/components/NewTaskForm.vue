<template>
  <form class="new_task_form" autocomplete="off">
    <label for="task">Task Name:</label>
    <input ref="task_name" type="text" name="task" />
    <button @click="addTask" type="button">Add Task</button>
  </form>
</template>
<script>
// constructor for a new task
const NewTask = (name) => {
  let complete = false;
  const completeTask = () => {
    complete = true;
  };
  const isComplete = () => {
    return complete;
  };
  return { name, completeTask, isComplete };
};

export default {
  props: ["project"],
  methods: {
    addTask() {
      // check if input is empty
      if (this.$refs.task_name.value === "") return;
      // create a NewTask object
      const task = NewTask(this.$refs.task_name.value);
      // add NewTask to list of tasks
      this.project.addTask(task);
      // clear input field and emit event
      this.$refs.task_name.value = "";
      this.$emit("closeTaskForm");
    },
  },
};
</script>
<style>
.new_task_form {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
</style>
