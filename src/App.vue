<template>
  <div id="app">
    <div class="navbar-header">
      <a class="navbar-brand">toDoList</a> 
      <input class="navbar-input" type="text" name="" placeholder="添加toDo" v-model="newText" @keydown="addText">
    </div>
    <div class="content">
      <h2>正在进行</h2>
      <div>
        <ul>
          <li v-for="(item, index) in list"  v-if="item.checked == false">
            <input  type="checkbox" class="check" v-model="item.checked">
            {{item.title}}
            <button @click="deleteText(index)">删除</button>
          </li>
        </ul>
      </div>
      <h2 >已经完成</h2>
      <div>
        <ul>
          <li v-for="(item, index) in list" v-if="item.checked == true">
            <input type="checkbox"  class="check" v-model="item.checked">
            {{item.title}}
            <button @click="deleteText(index)">删除</button>
          </li>
        </ul>
      </div>
    </div>
     <input type="checkbox" id="myCheck">
    <label for="myCheck"></label>
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
  body {
    margin: 0px;
    background-color: #C0C0C0;
  }
  .navbar-header {
    height: 50px;
    background-color: black;
  }
  .navbar-brand {
    float: left;
    height: 50px;
    padding: 15px;
    font-size: 18px;
    line-height: 20px;
    margin-left: 400px;
    color:#C0C0C0;
  }
  .navbar-input {
    display: inline-block;
    /*width: auto;*/
    vertical-align: middle;
    border-radius:4px;
    height: 20px;
    padding: 0px;
    font-size: 14px;
    line-height: 20px;
    /*border: 0px*/
    margin-top: 13px;
    margin-left: 150px;
  }
  .content {
    clear:both;
    margin-left: 400px;
  }
  .check {
    height: 20px;
    width: 20px;
  }

  ul>li {
    list-style: none; 
  }

</style>
