<template>
  <nav class="filter-nav">
    <button @click="sortFilter('all')" :class="{ active: currentFilter === 'all' }">All</button>
    <button @click="sortFilter('completed')" :class="{ active: currentFilter === 'completed' }">
      Completed
    </button>
    <button @click="sortFilter('ongoing')" :class="{ active: currentFilter === 'ongoing' }">
      Ongoing
    </button>
  </nav>
</template>

<script>
export default {
  props: ['currentFilter'],
  emits: ['filter-change'],
  methods: {
    sortFilter(filterBy) {
      this.$emit('filter-change', filterBy);
    },
  },
};
</script>

<style>
.filter-nav button {
  background: none;
  border: none;
  color: rgb(85, 84, 84);
  outline: none;
  font-size: 15px;
  margin-right: 10px;
  letter-spacing: 1px;
  font-weight: bold;
  cursor: pointer;
}
.filter-nav button.active {
  border-bottom: 3px solid #5cb5f0;
  padding-bottom: 4px;
}
</style>
