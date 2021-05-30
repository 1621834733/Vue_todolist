<template>
  <div class="todo-footer">
    <label>
      <input type="checkbox" v-model="checked" />
    </label>
    <span>
          <span >已完成{{finish}}</span> / 全部{{list.length}}
        </span>
    <button class="btn btn-danger" v-on:click="clear">清除已完成任务</button>
  </div>
</template>

<script>
    export default {
      name: "Footer",
      props:['list'],
      data(){
        return {
          length:0
        }
      },
      methods:{
      clear(){
        this.$bus.$emit('clear')
      }
      },
      computed:{
        finish(){
          this.length=this.list.reduce((adder,item)=>{
                  if(item.checked==true){
                    return adder+1
                  }
                  else return adder
          },0)
          return this.length
        },
        checked:{
          get(){
            if(this.length===this.list.length&&this.list.length!==0){
              return true
            }
          },
          set(){
              if(this.length<this.list.length&&this.list.length!==0){
                this.$bus.$emit('all',true)
              }else{
                this.$bus.$emit('all',false)
              }
          }
        }

      }
    }
</script>

<style scoped>
  .todo-footer {
    height: 40px;
    line-height: 40px;
    padding-left: 6px;
    margin-top: 5px;
  }

  .todo-footer label {
    display: inline-block;
    margin-right: 20px;
    cursor: pointer;
  }

  .todo-footer label input {
    position: relative;
    top: -1px;
    vertical-align: middle;
    margin-right: 5px;
  }

  .todo-footer button {
    float: right;
    margin-top: 5px;
  }
  .btn {
    display: inline-block;
    padding: 4px 12px;
    margin-bottom: 0;
    font-size: 14px;
    line-height: 20px;
    text-align: center;
    vertical-align: middle;
    cursor: pointer;
    box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.05);
    border-radius: 4px;
  }

  .btn-danger {
    color: #fff;
    background-color: #da4f49;
    border: 1px solid #bd362f;
  }

  .btn-danger:hover {
    color: #fff;
    background-color: #bd362f;
  }

  .btn:focus {
    outline: none;
  }
</style>
