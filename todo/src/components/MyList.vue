<template>
  <section>
    <transition-group name="list" tag="ul">
      <li v-for="(todoItem, index) in propsdata" :key="todoItem" class="shadow">
        <span class="checkButton"
          ><img src="../assets/check-sign.png" alt="check-sign"
        /></span>
        {{ todoItem }}
        <span
          class="removeBtn"
          type="button"
          @click="removeTodo(todoItem, index)"
          ><img src="../assets/delete-sign.png" alt="remove-sign" />
        </span>
      </li>
    </transition-group>
  </section>
</template>

<script>
export default {
  props: ["propsdata"],
  methods: {
    removeTodo(todoItem, index) {
      this.$emit("removeTodo", todoItem, index);
    },
  },
};
</script>

<style scoped>
ul {
  list-style-type: none;
  padding-left: 0px;
  margin-top: 0;
  text-align: left;
}
li {
  display: flex;
  min-height: 50px;
  height: 50px;
  line-height: 50px;
  margin: 0.5rem 0;
  padding: 0 0.9rem;
  background: white;
  border-radius: 10px;
}
.checkButton {
  line-height: 45px;
  color: #62acde;
  margin-right: 5px;
}
.checkButton img {
  margin-top: 15px;
  width: 20px;
}
.removeBtn {
  margin-left: auto;
  color: #de4343;
}
.removeBtn img {
  width: 50px;
}
.list-enter-active,
.list-leave-active {
  transition: all 1s;
}
.list-enter,
.list-leave-to {
  opacity: 0;
  transform: translateX(800px);
}
</style>
