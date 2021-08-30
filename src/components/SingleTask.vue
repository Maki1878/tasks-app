<template>
  <div class="task" :class="{ complete: task.complete }">
    <div class="actions">
      <h3 @click="showDetails = !showDetails">{{ task.title }}</h3>
      <div class="icons">
        <router-link :to="{ name: 'EditTask', params: { id: task.id } }">
          <span class="material-icons">
            edit
          </span>
        </router-link>
        <span @click="toggleComplete" class="material-icons done">
          done
        </span>
        <span @click="deleteTask" class="material-icons">
          delete
        </span>
      </div>
    </div>
    <div v-if="showDetails" class="details">
      <p>{{ task.details }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ['task'],
  emits: ['delete-task', 'toggle-complete'],
  data() {
    return {
      showDetails: false,
      uri: 'http://localhost:3000/tasks/' + this.task.id,
    };
  },
  methods: {
    deleteTask() {
      fetch(this.uri, {
        method: 'DELETE',
      })
        .then(() => this.$emit('delete-task', this.task.id))
        .catch((err) => console.log(err));
    },
    toggleComplete() {
      fetch(this.uri, {
        method: 'PATCH',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ complete: !this.task.complete }),
      })
        .then(() => this.$emit('toggle-complete', this.task.id))
        .catch((err) => console.log(err));
    },
  },
};
</script>

<style>
.task {
  margin: 20px auto;
  background: white;
  padding: 10px 25px;
  border-radius: 4px;
  box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.05);
  border-left: 8px solid #e70f7b;
}
h3 {
  cursor: pointer;
}
.actions {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.material-icons {
  font-size: 24px;
  margin-left: 10px;
  color: rgba(116, 112, 112, 0.986);
  cursor: pointer;
}
.material-icons:hover {
  color: rgb(26, 25, 25);
}
.task.complete {
  border-left: 8px solid #0abd81;
}
.task.complete .done {
  color: #0abd81;
}
</style>
