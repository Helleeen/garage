<template>
  <div id="app">
    <div class="container">
      <div class="col-md-6 offset-md-3">
        <h1 class="text-center mb-4">To Do</h1>
        <input type="text" class="form-control mb-4" v-model="userInput" @keyup.enter="addNewTodo">

        <div class="list-group mb-4">
          <template v-for="todo in activeTodoList">
            <todo
              v-bind:key="todo"
              :label="todo.label"
              @componentClick="toggleTodoStatus(todo)"
            />
          </template>
        </div>

        <div class="text-right">
          <button type="button" class="btn btn-sm" @click="changeCurrentStatus('active')">할 일</button>
          <button type="button" class="btn btn-sm" @click="changeCurrentStatus('done')">완료</button>
          <button type="button" class="btn btn-sm" @click="changeCurrentStatus('all')">전체</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Todo from './components/Todo';

export default {
  name: 'App',
  data(){
    return {
      userInput: '',
      todoList: [],
      currentStatus: 'active'
    };
  },
  computed: {
    activeTodoList(){
      return this.todoList.filter(todo => this.currentStatus === 'all' || todo.status === this.currentStatus);
    }
  },
  methods: {
    changeCurrentStatus(status){
      this.currentStatus = status;
    },
    addNewTodo(){
      this.todoList.push({
        label: this.userInput,
        status: 'active'
      });
      this.userInput= '';
    },
    toggleTodoStatus(todo){
      todo.status = todo.status === 'active' ? 'done' : 'active';
    }
  },
  components: {
    Todo
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
