<template>
  <div>
    <h1>List</h1>

    <div class="input-field col s12">
    <select ref="select" v-model="filter">
      <option value="" disabled selected>Choose your option</option>
      <option value="active">Active</option>
      <option value="outdated">Outdated</option>
      <option value="completed">Completed</option>
    </select>
    <label>Status filter</label>
    </div>

    <button v-if="filter" class="btn btn-small teal darken-3" @click="filter = null">Clear filter</button>

    <table v-if="tasks.length">
      <thead>
        <tr>
          <th>#</th>
          <th>Titile</th>
          <th>Date</th>
          <th>Description</th>
          <th>Status</th>
          <th>Open</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, idx) of displayTasks" :key="task.id">
          <td>{{ idx + 1 }}</td>
          <td>{{ task.title }}</td>
          <td>{{ new Date(task.date).toLocaleDateString() }}</td>
          <td class="description"><div class="text">{{ task.description }}</div></td>
          <td>{{ task.status }}</td>
          <td>
            <router-link tag="button" class="btn btn-small" :to="'/task/' + task.id">
            Open
            </router-link>
          </td>
        </tr>
      </tbody>
    </table>
    <p v-else>No tasks</p>
  </div>
</template>

<script>
export default {
  name: "List",
  data: () => ({
    filter: null,
  }),
  computed: {
    tasks() {
      return this.$store.getters.tasks;
    },
    displayTasks() {
      return this.tasks.filter(t => {
        if (!this.filter) {
          return true
        }
        return t.status === this.filter
      })
    }
  },
  mounted() {
    M.FormSelect.init(this.$refs.select)
  }
};
</script>

<style lang="scss" scoped>
.description {
  max-width: 400px;
}

.text {
  white-space: nowrap;
  text-overflow: ellipsis;
  overflow: hidden;
}
</style>