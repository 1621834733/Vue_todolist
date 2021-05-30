<template>
  <div id="app">
    <div class="todo-container">
      <div class="todo-wrap">
        <Header></Header>
        <List :list="todolist"></List>
        <Footer :list="todolist"></Footer>
      </div>
    </div>
  </div>
</template>
<script>
import Header from "./components/Header";
import List from "./components/List";
import Footer from "./components/Footer";
export default {
  name: 'App',
  components: {Footer, List, Header},
  data(){
    return {
      todolist:[
      ]
    }
  },
  methods:{
    add(item){
      this.todolist.push(item);
    },
    del(id){
      this.todolist=this.todolist.filter((item)=>{
        return item.id!==id
      })
    },
    check(id,check){
      this.todolist=this.todolist.filter((item)=>{
        if(item.id===id){
          item.checked=check
          return item
        }
        return item
      })
    },
    all(check){
      this.todolist=this.todolist.map((item)=>{
        item.checked=check
        return item
      })
    },
    clear(){
      this.todolist=this.todolist.filter((item)=>{
        return item.checked!==true
      })
    }
  },
  mounted() {
    this.$bus.$on('add',this.add)
    this.$bus.$on('del',this.del)
    this.$bus.$on('check',this.check)
    this.$bus.$on('all',this.all)
    this.$bus.$on('clear',this.clear)
    this.todolist=JSON.parse(localStorage.getItem('todolist'))||[]
  },
  watch:{
    todolist:{
      deep:true,
      handler(){
        localStorage.setItem('todolist',JSON.stringify(this.todolist))
      }
    }
  }
}

</script>

<style>
  body {
    background: #fff;
  }
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.todo-container {
  width: 600px;
  margin: 0 auto;
}
.todo-container .todo-wrap {
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
}

</style>
