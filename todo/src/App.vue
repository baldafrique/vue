<template>
  <div id="app">
    <MyHeader></MyHeader>
    <MyInput v-on:addTodo="addTodo"></MyInput>
    <MyList v-bind:propsdata="todoItems" @removeTodo="removeTodo"></MyList>
    <MyFooter v-on:removeAll="clearAll"></MyFooter>
    <input
      type="text"
      id="date"
      placeholder="Enter 8 digits of the D-Day (ex: 20211231)"
      v-model="dday"
    />
    <div id="dday"></div>
  </div>
</template>

<script>
import MyHeader from "./components/MyHeader.vue";
import MyInput from "./components/MyInput.vue";
import MyList from "./components/MyList.vue";
import MyFooter from "./components/MyFooter.vue";

export default {
  data() {
    return {
      todoItems: [],
      dday: "",
    };
  },
  watch: {
    dday: function (data) {
      if (data.length == 8) {
        var year = data.slice(0, 4);
        var month = data.slice(4, 6);
        var day = data.slice(6, 8);
        var today = new Date();
        var dday = new Date(year, month - 1, day);
        var gap = dday.getTime() - today.getTime();
        if (gap > 0) {
          var result = Math.ceil(gap / (1000 * 60 * 60 * 24));
          document.querySelector("#dday").innerHTML = `day-${result}`;
        } else {
          document.querySelector(
            "#dday"
          ).innerHTML = `Enter the date after ${today.getFullYear()}-${today.getMonth()}-${today.getDate()}`;
        }
      } else {
        document.querySelector("#dday").innerHTML = "It's not 8 digits";
      }
    },
  },
  methods: {
    clearAll() {
      localStorage.clear();
      this.todoItems = [];
    },
    addTodo(todoItem) {
      localStorage.setItem(todoItem, todoItem);
      this.todoItems.push(todoItem);
    },
    removeTodo(todoItem, index) {
      localStorage.removeItem(todoItem);
      this.todoItems.splice(index, 1);
    },
  },
  created() {
    if (localStorage.length > 0) {
      for (var i = 0; i < localStorage.length; i++) {
        this.todoItems.push(localStorage.key(i));
      }
    }
  },
  components: {
    MyHeader: MyHeader,
    MyInput: MyInput,
    MyList: MyList,
    MyFooter: MyFooter,
  },
};
</script>

<style>
body {
  text-align: center;
  background-color: #f6f6f8;
}
input {
  border-style: groove;
  width: 200px;
}
button {
  border-style: groove;
}
.shadow {
  box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
}
#date {
  background: rgb(194, 193, 193);
  border-style: none;
  font-size: 1rem;
  width: 400px;
  height: 50px;
  border-radius: 15px;
  text-align: center;
  margin-top: 1rem;
}
#dday {
  padding-top: 15px;
  font-size: 2.5rem;
  font-weight: 300;
}
</style>
