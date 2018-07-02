<template>
  <div id="app">
    <div class="navbar-header">
      <a class="navbar-brand">toDoList</a> 
      <input class="navbar-input" type="text" name="" placeholder="添加toDo" v-model="newText" @keydown="addText">
    </div>
    <div class="content">
      <h2>正在进行</h2>
      <span>{{processCnt}}</span>
      <div>
        <ul>
          <li v-for="(item, index) in list"  v-if="item.checked == false">
            <input  type="checkbox" class="check" v-model="item.checked">
            {{item.title}}
            <img src="./assets/delete.png" @click="deleteText(index)">
          </li>
        </ul>
      </div>
      <h2 >已经完成</h2>
      <span>{{finishCnt}}</span>
      <div>
        <ul>
          <li v-for="(item, index) in list" v-if="item.checked == true">
            <input type="checkbox"  class="check" v-model="item.checked">
            {{item.title}}
            <img src="./assets/delete.png" @click="deleteText(index)">
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import storage from './module/storage.js';

export default {
  name: 'app',
  data () {
    return {
      list:[],
      newText:"",
      processCnt:0,
      finishCnt:0,
    }
  },
  methods:{
    addText(event) {
      if ((event.type == "click" || event.keyCode == 13) && this.newText.trim() != "") {
        var newItem = {'title':this.newText,'checked':false};
        this.list.push(newItem);
        this.newText = "";    
      }
    },
    deleteText(index) {
      this.list.splice(index,1);
    }
  },
  mounted:function() {
    var list = storage.get('list');
    if (list) {
      this.list = list;
    }
  },
  watch: {
    list: {
      handler: function (newVal, oldVal) {
        var finishCnt = 0;
        var allCnt = newVal.length;
        for (var i = 0; i < allCnt; i++) {
          var item = newVal[i];
          if (item.checked) {
            finishCnt += 1;
          }
        }
        this.finishCnt = finishCnt;
        this.processCnt = allCnt - finishCnt;
        storage.set('list',this.list);   
      },
      deep: true
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
    margin-left: 40px;
    width: 320px;
  }
  .content {
    clear:both;
    margin-left: 400px;
  }
  .check {
    height: 20px;
    width: 20px;
    vertical-align:middle;
    margin-top:0px;
  }

  h2 {
    display: inline-block;
  }

  span {
    width: 20px;
    height: 20px;
    border-radius:20px;
    background-color: #D3D3D3;
    line-height: 20px;
    font-size: 15px;
    margin-left: 300px;
  }


  ul {
    padding-left: 0px;
  }

  li {
    list-style: none;
    width: 450px;
    background-color: #FFFFFF;
    margin-bottom: 5px;
    margin-top: 5px;
    padding-left:  5px;
    padding-right:  5px;
    border-left: 5px solid #008080;
    border-radius:2px;
    height:30px;
    line-height: 30px;
    vertical-align: middle;
  }

  li img {
    float: right;
    width: 18px;
    height: 18px;
    margin-top: 5px;
  }

</style>
