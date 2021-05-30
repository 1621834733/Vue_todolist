<template>
    <li :class="line">
      <label>
        <input type="checkbox" v-model="checked"/>
        <span>{{item.content}}</span>
      </label>
      <button class="btn btn-danger" v-on:click="del">删除</button>
    </li>

</template>

<script>
    export default {
      props:['item'],
      name: "Item",
      methods:{
        del(){
          this.$bus.$emit('del',this.item.id)
        }
      },
      computed:{
        checked:{
          get(){
            return this.item.checked
          },
          set(){
            this.$bus.$emit('check',this.item.id,!this.item.checked)
          }
        },
        line(){
          if(this.item.checked===true){
            return 'line'
          }
        }
      }
    }
</script>

<style scoped>
  li {
    list-style: none;
    height: 36px;
    line-height: 36px;
    padding: 0 5px;
    border-bottom: 1px solid #ddd;
    position: relative;
  }
  .line:after{
    content: '';
    width: 100%;
    height: 3px;
    background-color: red;
    position: absolute;
    top:50%;
    left: 0;
  }{

  }
li:hover button{
  display: inline-block;
}
  li label {
    float: left;
    cursor: pointer;
    margin-bottom: 0;
  }

  li label li input {
    vertical-align: middle;
    margin-right: 6px;
    position: relative;
    top: -1px;
  }

  li button {
    float: right;
    display: none;
    margin-top: 3px;
  }

  li:before {
    content: initial;
  }

  li:last-child {
    border-bottom: none;
  }
  .btn {
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
