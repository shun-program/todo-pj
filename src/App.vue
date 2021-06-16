<template>
  <div class="app">
    <div class="todo">
      <div class="title">
      <h1>Todo List</h1>
      </div>
      <div class="aaa">
        <input type="text" class="input-add" name="name" id="name" v-model="newTodo" />
         <button class="add" @click="insertTodo">追加</button>
      </div>
      <div v-for="item in todoLists" :key="item.id">
      <input class="input-update" type="text" v-model="item.name" />
      <div class="button">
       <button class="update" @click="updateTodo(item.id, item.name)">更新</button>
       <button class="delete" @click="deleteTodo(item.id)">削除</button>
      </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      newTodo: "",
      todoLists: [],
    };
  },
  methods: {
    async getTodo() {
      const resData = await axios.get("https://murmuring-reef-20196.herokuapp.com/api/todo");
      this.todoLists = resData.data.data;
      this.newTodo = "";
    },
    async insertTodo() {
      const sendData = {
        name: this.newTodo,
      };
      await axios.post("https://murmuring-reef-20196.herokuapp.com/api/todo", sendData);
      await this.getTodo();
    },
    async updateTodo(id, name) {
      const sendData = {
        name: name,
      };
      await axios.put("https://murmuring-reef-20196.herokuapp.com/api/todo/" + id, sendData);
      await this.getTodo();
    },
    async deleteTodo(todo) {
      await axios.delete("https://murmuring-reef-20196.herokuapp.com/api/todo/" + todo);
      await this.getTodo();
    },
  },
  created() {
    this.getTodo();
  },
};
</script>

<style>
@charset "UTF-8";

/*
html5doctor.com Reset Stylesheet
v1.6.1
Last Updated: 2010-09-17
Author: Richard Clark - http://richclarkdesign.com
Twitter: @rich_clark
*/

html, body, div, span, object, iframe,
h1, h2, h3, h4, h5, h6, p, blockquote, pre,
abbr, address, cite, code,
del, dfn, em, img, ins, kbd, q, samp,
small, strong, sub, sup, var,
b, i,
dl, dt, dd, ol, ul, li,
fieldset, form, label, legend,
table, caption, tbody, tfoot, thead, tr, th, td,
article, aside, canvas, details, figcaption, figure,
footer, header, hgroup, menu, nav, section, summary,
time, mark, audio, video {
    margin:0;
    padding:0;
    border:0;
    outline:0;
    font-size:100%;
    vertical-align:baseline;
    background:transparent;
}

body {
    line-height:1;
}

article,aside,details,figcaption,figure,
footer,header,hgroup,menu,nav,section {
    display:block;
}

nav ul {
    list-style:none;
}

blockquote, q {
    quotes:none;
}

blockquote:before, blockquote:after,
q:before, q:after {
    content:'';
    content:none;
}

a {
    margin:0;
    padding:0;
    font-size:100%;
    vertical-align:baseline;
    background:transparent;
}

/* change colours to suit your needs */
ins {
    background-color:#ff9;
    color:#000;
    text-decoration:none;
}

/* change colours to suit your needs */
mark {
    background-color:#ff9;
    color:#000;
    font-style:italic;
    font-weight:bold;
}

del {
    text-decoration: line-through;
}

abbr[title], dfn[title] {
    border-bottom:1px dotted;
    cursor:help;
}

table {
    border-collapse:collapse;
    border-spacing:0;
}

/* change border colour to suit your needs */
hr {
    display:block;
    height:1px;
    border:0;  
    border-top:1px solid #cccccc;
    margin:1em 0;
    padding:0;
}

input, select {
    vertical-align:middle;
}

/* ///////////////////////////////////// */

.app {
  min-height: 100vh;
  background-color: #2D197C;
  
}

.todo{
  background-color: #fff;
  width: 50vw;
  padding: 30px;
  position: absolute;   
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  border-radius: 10px
}

.title {
  font-size: 24px;
  margin-bottom: 5px;
}
.add {
  text-align: left;
  border: 2px solid #DC70FA;
  font-size: 12px;
  color: #DC70FA;
  background-color: #fff;
  font-weight: bold;
  padding: 8px 16px;
  border-radius: 5px;
  cursor: pointer;
  transition: 0.5s;
  float: right;
  margin-top: 10px;
  margin-bottom: 10px;  
}

.add:hover {
  border: 2px solid #DC70FA;
  font-size: 12px;
  color: #FFF;
  background-color: #DC70FA;
}

.input-add {
  width: 80%;
  padding: 10px 0px 10px 5px;;
  border-radius: 5px;
  border: 1px solid #ccc;
  font-size: 14px;
  appearance: none;
  outline: none;
  margin-top: 10px;
  margin-bottom: 10px;  
}

.input-update {
  width: 30%;
  padding: 10px 0px 10px 5px;;
  border-radius: 5px;
  border: 1px solid #ccc;
  font-size: 14px;
  appearance: none;
  outline: none;
  margin-top: 5px;
}

.button {
  float: right;
}

.update {
  text-align: left;
  border: 2px solid #FA9770;
  font-size: 12px;
  color: #FA9770;
  background-color: #fff;
  font-weight: bold;
  padding: 8px 16px;
  border-radius: 5px;
  cursor: pointer;
  transition: 0.4s;
  outline: none;
  margin-top: 5px;
}
.update:hover {
  border: 2px solid #FA9770;
  font-size: 12px;
  color: #FFF;
  background-color: #FA9770;
}

.delete {
  text-align: left;
  border: 2px solid #71FADC;
  font-size: 12px;
  color: #71FADC;
  background-color: #fff;
  font-weight: bold;
  padding: 8px 16px;
  border-radius: 5px;
  cursor: pointer;
  transition: 0.4s;
  outline: none;
  margin-top: 5px;
  margin-left: 5px;
}

.delete:hover {
  border: 2px solid #71FADC;
  font-size: 12px;
  color: #FFF;
  background-color: #71FADC;
}

@media screen and (max-width : 768px){

}

</style>