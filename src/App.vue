<template>
   <div class="container">
    <h1>工资表</h1>
    <div class="add">
      <input type="text" name="username" v-model="newUser.username" placeholder="姓名" />
      <input type="text" name="position" v-model="newUser.position" placeholder="职位" />
      <input type="date" name="birth" v-model="newUser.birth" placeholder="生日" />
      <input type="number" name="salary" v-model="newUser.salary" placeholder="薪水" number/>
      <button v-on:click="addItem">新增</button>
    </div>
    <section class="list">
      <ul class="user-list">
        <li class="user" v-for="user in users" :class="{editing: user == editedUser}">
          <div class="view">
            <label @dblclick="editItem(user)">{{user.username}}</label>
            <input class="edit" type="text" v-model="user.username" @blur="doneEdit(user)"
              @keyup.enter="doneEdit(user)"/>
            <label @dblclick="editItem(user)">{{user.position}}</label>
            <input class="edit" type="text" v-model="user.position" @blur="doneEdit(user)"
              @keyup.enter="doneEdit(user)"/>
            <label @dblclick="editItem(user)">{{user.birth}}</label>
            <input class="edit" type="date" v-model="user.birth" @blur="doneEdit(user)"
              @keyup.enter="doneEdit(user)"/>
            <label @dblclick="editItem(user)">{{user.salary}}</label>
            <input class="edit" type="number" v-model="user.salary" @blur="doneEdit(user)"
              @keyup.enter="doneEdit(user)" number/>
            <button class="destroy" v-on:click="removeItem(user)">删除</button>
          </div>
        </li>
      </ul>
    </section>
   </div>
</template>

<script>
export default {
  data () {
    return {
      newUser: {},
      users: [
        {
          username: 'mrdream',
          position: 'front-end',
          birth: '1991-7-17',
          salary: '1000'
        }
      ],
      editedUser: null
    }
  },
  methods: {
    addItem: function () {
      var value = this.newUser;
      if (!value.username || !value.position || !value.birth || !value.salary) {
        alert("有选项未填");
        return;
      }
      if(value.username.length > 9 || value.position.length > 9){
        alert("输入项太长了。。");
        return;
      }
      this.users.push(value);
      this.newUser = '';
    },
    editItem: function (user) {
      this.editedUser = user;
    },
    doneEdit: function (user) {
      if (!this.editedUser) {
        return;
      }  
      if (!user.username || !user.position || !user.birth || !user.salary) {
        alert('有选项未填');
        return;
      }
      if(user.username.length > 9 || user.position.length > 9){
        alert("输入项太长了。。");
        return;
      }
      this.editedUser = null; 
    },
    removeItem: function (user) {
      this.users.$remove(user);
    }
  }
}
</script>

<style>
  .container{
    width:800px;
    margin: auto;
    padding-bottom:50px;
    background-color:#FAFAFA;
  }
  h1{
    text-align:center;
    font-size:40px;
    line-height:100px;
    color:#888;
  }
  .add{
    width:100%;
    height:50px;
    /*background-color:#ccc;*/
    margin-bottom:40px;
    text-align:center;
    padding:10px 0;
    box-sizing:border-box;
  }
  .add input{
    width:150px;
    height:35px;
    margin:0 5px;
    border-radius:3px;
    border: 1px solid #EDEEEE;
    padding:5px 10px;
    box-sizing:border-box;
    outline: none;
    transition:all 0.2s ease-in;
  }
  .add input:focus{
    border-radius:15px;
    transition:all 0.2s ease-in;
  }
  button{
    width:100px;
    height:30px;
    background-color:#00CE96;
    text-align:center;
    font-size:14px;
    color:#fff;
    border: none;
    border-radius:30px;
    cursor:pointer;
    transition:all 0.2s ease-out;
  }
  button:hover{
    background-color:#fff;
    border: 1px solid #00CE96;
    color:#00CE96;
    transition:all 0.2s ease-in;
  }
  .list{
    width:100%;
    text-align:center;
  }
  .user{
    margin-bottom:20px;
  }
  .view label{
    width:150px;
    height:40px;
    text-align:center;
    border:1px solid #888;
    line-height:40px;
    font-size:15px;
    display:inline-block;
  }
  .edit{
    display:none;
  }
  .editing .edit{
    display:inline-block;
    width:148px;
    height:38px;
    text-align:center;
    border:1px solid #888;
    line-height:38px;
    font-size:15px;
    outline:none;
  }
  .editing label{
    display:none;
  }
  button.destroy{
    width:80px;
    background-color:#E02F6F;
    border-radius:5px;
  }
  button.destroy:hover{
    background-color:#fff;
    border: 1px solid #E02F6F;
    color:#E02F6F;
    transition:all 0.2s ease-in;
  }
</style>