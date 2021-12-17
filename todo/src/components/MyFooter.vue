<template>
  <div class="Container">
    <span class="deleteAllButton" @click="deleteToDo">Delete All</span>
  </div>
</template>

<script>
export default {
  methods: {
    deleteToDo() {
      this.$emit("removeAll");
    },
  },
};
</script>

<style scoped>
.Container {
  width: 7rem;
  height: 35px;
  line-height: 35px;
  background-color: red;
  border-radius: 5px;
  margin: 0 auto;
}
.deleteAllButton {
  color: white;
  font-size: 1.3rem;
  font-weight: 500;
  display: block;
}
</style>
