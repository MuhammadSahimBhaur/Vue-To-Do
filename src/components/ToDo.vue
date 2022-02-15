<template>
  <div>
    <h1>To Do App</h1>
    <input type="text" v-model="task" />
    <button @click="handleSubmit(task)">SUBMIT</button>
    <div>
      <table></table>
      <table>
        <thead>
          <th>Index</th>
          <th>Task</th>
          <th>Status</th>
        </thead>
        <tbody v-for="(task, index) in tasks" :fields="fields" :key="task">
          <tr>
            <td>{{ index + 1 }}.</td>
            <td>{{ task.task }}</td>
            <td>{{ task.status }}</td>
            <button @click="handleEdit(index)">edit</button>
            <button @click="handleDelete(index)">delete</button>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isEdit: false,
      index: null,
      task: null,
      fields: ["task", "status"],
      tasks: [],
    };
  },

  methods: {
    handleSubmit(new_task) {
      console.log(new_task);
      if (this.isEdit === false) {
        this.tasks.push({ task: new_task, status: "to-do" });
        this.task = null;
      } else {
        this.tasks[this.index].task = new_task;
        this.isEdit = false;
        this.index = null;
      }
    },
    handleDelete(index) {
      this.tasks.splice(index, 1);
    },
    handleEdit(old_index) {
      this.isEdit = true;
      this.index = old_index;
      this.task = this.tasks[this.index].task;
    },
  },
};
</script>

<style >
</style>
