<template>
  <div id="app">
    <input type="text" name="" v-model="newText">
    <button @click="addText()">添加</button>
    <br>
    <hr>
    <br>
    <ul>
      <li v-for="(item, index) in list">
        {{item.text}}
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
    addText() {
      if (this.newText.trim() != "") {
        var newItem = {'text':this.newText};
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
