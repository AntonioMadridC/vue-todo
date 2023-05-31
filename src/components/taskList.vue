<template>
  <section>
    <h1>TO-DO list</h1>
    <div v-if="!edit">
      <input type="text" v-model="task" />
      <input
        type="submit"
        value="Agregar"
        @click="addTask"
        :disabled="task == ''"
      />
    </div>
    <div v-else>
      <input type="text" v-model="task" />
      <input
        type="submit"
        value="Actualizar"
        @click="updateTask"
        :disabled="task == ''"
      />
    </div>
    <div class="container">
      <ol>
        <li v-for="(task, index) in tasks" :key="task">
          {{ task }}
          <button @click="editTask(index, task)">Edit</button>
          <button @click="removeTask(index)">Delete</button>
        </li>
      </ol>
    </div>
  </section>
</template>

<script>
export default {
  name: "task-list",
  // props: {},
  data: function () {
    return {
      tasks: [],
      task: "",
      edit: false,
    };
  },
  // computed: {},
  methods: {
    addTask() {
      this.tasks.push(this.task);
      this.task = "";
    },
    removeTask(index) {
      this.tasks.splice(index, 1);
    },
    editTask(index, task) {
      this.edit = true;
      this.task = task;
      this.selectedIndex = index;
    },
    updateTask() {
      this.tasks.splice(this.selectedIndex, 1, this.task);
      this.task = "";
      this.edit = false;
    },
  },
  // watch: {},
  // components: {},
  // mixins: [],
  // filters: {},
  // -- Lifecycle Methods
  // -- End Lifecycle Methods
};
</script>

<style scoped>
ol {
  text-align: start;
}
.container {
  width: 50%;
  margin: 0 auto;
}
</style>