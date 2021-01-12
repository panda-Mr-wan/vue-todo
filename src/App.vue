<template>
  <section class="todoapp">
    <header class="header">
      <h1>Todos</h1>
      <input type="text" class="new-todo" v-model.trim="todoList" @keyup.enter="addTodo">
    </header>
    <section class="main">
      <input type="checkbox" class="toggle-all" id="toggle-all" v-model="isAll">
      <label for="toggle-all"></label>
      <ul class="todo-list">
        <Item v-for="(value,index) in filterTodoDatas" :index="index" :key="value.id" :todo="value" />
      </ul>
    </section>
    <Footer :todoNum="todoNum" :view="view" />
  </section>
</template>

<script>
  import Item from "./components/Item";
  import Footer from "./components/Footer";
  export default {
    name:"App",
    components:{ Item, Footer },
    data(){
      return {
        todoDatas:[],
        todoList:"",
        view:"all"
      }
    },
    methods:{
      addTodo(){
        if(this.todoList=="") return false;
        let todo={};
        let id=new Date().getTime();
        todo={id:id,value:this.todoList,hasCompleted:false};
        this.todoDatas.push(todo);
        this.todoList=""
      }
    },
    computed:{
      todoNum(){
        return this.todoDatas.filter((value) => {
          return !value.hasCompleted;
        }).length
      },
      isAll:{
        get(){
          return this.todoNum===0;
        },
        set(val){
          this.todoDatas.map((value) => {
            value.hasCompleted=val;
            return value
          })
        }
      },
      filterTodoDatas(){
        switch(this.view){
          case "all":
            return this.todoDatas;
          case "active":
            return this.todoDatas.filter((value) => {
              return !value.hasCompleted;
            })
          case "completed":
            return this.todoDatas.filter((value) => {
              return value.hasCompleted;
            })
          default:
            return this.todoDatas;
        }
      }
    }
  }
</script>

<style lang="scss" scoped>

</style>