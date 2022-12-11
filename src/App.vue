<template>
  <div id="app">
    <TodoHeader1>
     
    </TodoHeader1>
    <TodoInput1 v-on:addTodoItem="addOneItem"></TodoInput1>
    <TodoList v-bind:propsdata="todoItems" v-on:removeItem="removeOneItem"></TodoList>
    <TodoFooter>
        
    </TodoFooter>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoInput from './components/TodoInput.vue'
import TodoList from './components/TodoList.vue'
import TodoFooter from './components/TodoFooter.vue'

export default {
  data: function() {
    return {
      todoItems: []
    }
  },
  methods: {
    addOneItem: function(todoItem) {
      var obj = {completed: false, item: todoItem};
      localStorage.setItem(todoItem,JSON.stringify(obj));
      this.todoItems.push(obj);
    },
    removeOneItem: function(todoItem, index) {
      localStorage.removeItem(todoItem.item);
      this.todoItems.splice(index, 1);
    },
  },
  created: function() {
        if (localStorage.length > 0) {
            for (var i=0; i < localStorage.length; i++) {
                 this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i)))); 
            }
        }
  },
  components: {
    "TodoHeader1": TodoHeader, // 앞에 이름이 template에서 사용되는 이름
    "TodoInput1": TodoInput,
    TodoList,                 // ES6+    
    TodoFooter,
  }
}
</script>

<style>
body {
  text-align: center;
  background-color:#f6f6f6;
}
input {
  border-style: groove;
  width: 200px;
}
button {
  border-style: groove;
}

.shadow {
  box-shadow: 5px 10px 10px rgb(0,0,0,0.03);
}
</style>
