<template>
  <div id="app">
    <h1>ToDoリスト</h1>
    <div>
      <form>
        <label><input type="radio" value="all" v-model="radioStatus" checked="true">すべて</label>
        <label><input type="radio" value="working" v-model="radioStatus">作業中</label>
        <label><input type="radio" value="complete" v-model="radioStatus">完了</label>
      </form>
    </div>
    <div>
      <table>
        <thead>
          <tr>
            <th>ID</th>
            <th>コメント</th>
            <th>状態</th>
            <th></th>
          </tr>
        </thead>

        <tbody>
          <tr v-for="(todo) in todos" :key="todo">
            <th>{{ todos.indexOf(todo) }}</th>
            <th>{{ todo.text }}</th>
            <th><button v-bind:class="todo.state" v-on:click="change(todos.indexOf(todo))">{{ changeStatus(todo.state) }}</button></th>
            <th><button id="remove" v-on:click="removeTodo(todos.indexOf(todo))">削除</button></th>
          </tr>  
        </tbody>
      </table>
    </div>
    <div>
      <h2>新規タスクの追加</h2>
      <input type="text" v-model.trim="addtext" placeholder="すること">
      <button v-on:click="addTodo">追加</button>
    </div>
  </div>
</template>

<script>
export default {
  data: function(){
    return{
      radioStatus: "",
      index: 0,
      addtext: "",
      todos: []
    }
  },

  methods: {
  //作業中・完了ボタンが押されたとき
    change: function(el) {
      if(this.todos[el].state === "work"){
        this.$set(this.todos[el],"state","end");
      }else{
        this.$set(this.todos[el],"state","work");
      }
    },

    //ボタンの表記
    changeStatus: function(el) {
      if(el === "work"){
        return "作業中";
      }else{
        return "完了";
      }
    },

    //タスクの追加
    addTodo: function(){
      this.todos.push({id:this.index, text:this.addtext, state:"work"});
      this.addtext = '';
      this.index++;
    },

    //タスクの削除
    removeTodo: function(el) {
      this.todos.splice(el, 1);
      this.index--;
    }
  }
}
</script>