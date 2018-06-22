<template>
  <div id="app">
    <input type="text" name="" v-model="newText" @keydown="addText">
    <!-- <button @click="addText">添加</button> -->
    <br>
    <hr>
    <h2>进行中</h2>
    <ul>
      <li v-for="(item, index) in list"  v-if="item.checked == false">
        <input type="checkbox" v-model="item.checked">
        {{item.title}}
        <button @click="deleteText(index)">删除</button>
      </li>
    </ul>
    <h2>已完成</h2>
    <ul>
      <li v-for="(item, index) in list" v-if="item.checked == true">
        <input type="checkbox" v-model="item.checked">
        {{item.title}}
        <button @click="deleteText(index)">删除</button>
      </li>
    </ul>

  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      list:[],
      newText:"",
    }
  },
  methods:{
    addText(event) {
      console.log(event);
      if ((event.type == "click" || event.keyCode == 13) && this.newText.trim() != "") {
        var newItem = {'title':this.newText,'checked':false};
        this.list.push(newItem);
        this.newText = "";      
      }
    },
    deleteText(index) {
      this.list.splice(index,1);
    }
  }
}
</script>

<style>
</style>
