<template>
  <div class="inputBox shadow">
    <input
      type="text"
      v-model="newTodoItem"
      placeholder="What's new task?"
      v-on:keypress.enter="addTask"
    />
    <span class="addContainer" v-on:click="addTask">
      <button class="addButton">+</button>
    </span>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTodoItem: "",
    };
  },
  methods: {
    addTask
    () {
      if (this.newTodoItem !== "") {
        var value = this.newTodoItem && this.newTodoItem.trim();
        this.$emit("addTask
        ", value);
        localStorage.setItem(value, value);
        this.clearInput();
      }
    },
    clearInput() {
      this.newTodoItem = "";
    },
  },
};
</script>

<style scoped>
input:focus {
  outline: none;
}
.inputBox {
  background: rgb(194, 193, 193);
  height: 45px;
  line-height: 45px;
  border-radius: 15px;
}
.inputBox input {
  background: rgb(194, 193, 193);
  border-style: none;
  font-size: 1rem;
}
.addContainer {
  float: right;
  background: black;
  display: inline-block;
  width: 3rem;
  border-radius: 0 5px 5px 0;
}
.addButton {
  color: white;
  background: black;
  border: none;
  font-size: 2.2rem;
  vertical-align: middle;
}
</style>
