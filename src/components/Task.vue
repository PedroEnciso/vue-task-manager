<template>
  <div class="task">
    <input
      v-if="checked"
      @click="markBoxAsChecked"
      type="checkbox"
      checked="checked"
      name="{{ task.name }}"
    />
    <input
      v-else
      @click="markBoxAsChecked"
      type="checkbox"
      name="{{ task.name }}"
    />

    <label for="{{task.name}}">{{ task.name }}</label>
  </div>
</template>
<script>
export default {
  props: ["task"],
  methods: {
    markBoxAsChecked() {
      this.checked = true;
      this.task.completeTask();
    },
  },
  data() {
    return {
      checked: false,
    };
  },
};
</script>
<style>
.task {
  width: 100%;
  display: grid;
  margin-top: 5px;
  grid-template-columns: 1fr 4fr;
  align-items: center;
  color: #2c3e50;
}

.task input {
  justify-self: end;
  margin-right: 8px;
  border-radius: 20px;
}

.task input:checked {
  display: none;
}

.task label {
  text-transform: lowercase;
  grid-column: 2/3;
}

.task input:checked + label {
  color: #d3d3d3;
  text-decoration: line-through;
}
</style>
