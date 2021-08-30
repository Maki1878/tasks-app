<template>
  <div class="home">
    <FilterNav @filter-change="currentFilter = $event" :currentFilter="currentFilter" />
    <div v-if="tasks.length">
      <div v-for="task in filteredTasks" :key="task.id">
        <SingleTask :task="task" @delete-task="deleteTask" @toggle-complete="toggleComplete" />
      </div>
    </div>
  </div>
</template>

<script>
import SingleTask from '../components/SingleTask.vue';
import FilterNav from '../components/FilterNav.vue';

export default {
  name: 'Home',
  components: {
    SingleTask,
    FilterNav,
  },
  data() {
    return {
      tasks: [],
      currentFilter: 'all',
    };
  },
  mounted() {
    fetch('http://localhost:3000/tasks')
      .then((res) => res.json())
      .then((data) => (this.tasks = data))
      .catch((err) => console.log(err.message));
  },
  methods: {
    deleteTask(id) {
      this.tasks = this.tasks.filter((task) => task.id !== id);
    },
    toggleComplete(id) {
      const task = this.tasks.find((task) => task.id === id);
      task.complete = !task.complete;
    },
  },
  computed: {
    filteredTasks() {
      if (this.currentFilter === 'completed') {
        return this.tasks.filter((task) => task.complete);
      }
      if (this.currentFilter === 'ongoing') {
        return this.tasks.filter((task) => !task.complete);
      }
      return this.tasks;
    },
  },
};
</script>
