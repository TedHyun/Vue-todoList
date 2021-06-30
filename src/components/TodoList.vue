<template>
  <div>
      <ul>
        <li>------</li>
        <li v-for="(todoItem, index) in todoItems" v-bind:key="todoItem" class="shadow">
          <i class="far fa-check-square" v-bind:class="{checkBtnCompleted: todoItems.completed}" v-on:click="toggleComplete(todoItem, index)"></i>/
          <span v-bind:class="{textCompleted: todoItem.completed}">{{todoItem.item}}</span>
          <span class="removeBtn" v-on:click="removeTodo(todoItem, index)">
          <i class="fas fa-trash"></i>
          </span>
          </li>
        <li>------</li>
        
      </ul>
  </div>
</template>

<script>
export default {
data: function() {  
    return {
      todoItems: []
    }
},
  methods: {
    removeTodo: function(todoItem,index) {
      console.log(todoItem, index);
      localStorage.removeItem(todoItem);
      this.todoItems.splice(index,1);
    },
    toggleComplete: function(todoItem,index) {
        todoItem.completed =! todoItem.completed;
        //local stroage 데이터 갱신
        localStorage.removeItem(todoItem,item);
        localStorage.setItem(todoItem,item, JSON.stringify(todoItem));
  }
},
created: function() {
  if(localStorage.length > 0) {
    for (var i = 0; i < localStorage.length; i ++){
       
      //console.log(JSON.parse(localStorage.getItem(localStorage.key(i))));
      this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));

      //this.todoItems.push(localStorage.key(i));
      //console.log(localStorage.key(i));
    }
  }
  //console.log( this.todoItems.push(localStorage.key(i)));
  }
}

</script>

<style scoped>
ul {
  list-style-type: none;
  padding-left: 0px;
  margin-top: 0;
  text-align: left;
}
li {
  display: flex;
  min-height: 50px;
  height: 50px;
  line-height: 50px;
  margin: 0.5rem 0;
  padding: 0 0.9rem;
  background: white;
  border-radius: 5px;
}
.checkBtn{
  line-height: 45px;
  color: #62acde;
  margin-right: 5px;
}
.checkBtnCompleted {
  color: #b3adad;
}
.textCompleted {
  text-decoration: line-through;
  color: #b3adad;
}
.removeBtn {
  margin-left: auto;
  color: #de4343;
}
</style>