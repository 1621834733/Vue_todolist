<template>
  <div>
  <ul class="todo-main" v-for="item in list">
      <Item :item="item"></Item>
  </ul>
    </div>
</template>

<script>

    import Item from "./Item";
    export default {
      props:['list'],
      name: "List",
      components: {Item}
    }
</script>

<style scoped>
  .todo-main {
    margin-left: 0px;
    border: 1px solid #ddd;
    border-radius: 2px;
    padding: 0px;
  }

</style>
