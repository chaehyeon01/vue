<template>
  <div id="app">
    <TodoHeader></TodoHeader>
    <TodoInput v-on:addTodoItem="addOneItem"></TodoInput>
    <TodoList v-bind:propsdata="todoItems" v-on:toggleItem="toggleOneItem" v-on:removeItem="removeOneItem"></TodoList>
    <TodoFooter v-on:clearAll="clearAllItems"></TodoFooter>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoInput from './components/TodoInput.vue'
import TodoList from './components/TodoList.vue'
import TodoFooter from './components/TodoFooter.vue'

export default {
  data: function(){
    return {
      todoItems:[]
    }
  },
  methods:{
    addOneItem:function(todoItem){
       //하위 컴포넌트에서 발생한 이벤트에서 todoItem을 받아옴. 
        const obj={completed:false, item:todoItem};
        //로컬스토리지 저장 
        localStorage.setItem(todoItem,JSON.stringify(obj));
        this.todoItems.push(obj);
    },
    removeOneItem:function(todoItem, index ) {
      localStorage.removeItem(todoItem.item);
      this.todoItems.splice(index,1); //어떤배열에서 어떤 자리에 있는 데이터를 하나 지우겠다.
    },
    toggleOneItem: function(todoItem, index ){

//로컬스트리지 데이타 갱신
      // todoItem.completed= !todoItem.completed;
      this.todoItems[index].completed = !this.todoItems[index].completed;
      localStorage.removeItem(todoItem.item);
      localStorage.setItem(todoItem.item,JSON.stringify(todoItem));
    },
    clearAllItems:function(){
      localStorage.clear();
      this.todoItems =[];
    }
  },
  created:function (){
    if(localStorage.length>0){
      for(let i=0; i <localStorage.length; i++){
        if(localStorage.key(i) !== 'loglevel:webpack-dev-server' && localStorage.key(i) !=='randid' ){
         let data=JSON.parse(localStorage.getItem(localStorage.key(i)));
         console.log(data);
          this.todoItems.push(data);
        }
          // console.log(localStorage.key(i));
      } 
    }
  },
  components: {
    'TodoHeader':TodoHeader,
    'TodoInput' :TodoInput,
    'TodoList' :TodoList,
    'TodoFooter' :TodoFooter
  }
}
</script>

<style>
body {
  text-align: center;
  background-color:#F6F6F6;
}
input {
  border-style: groove;
  width: 200px;
}
.shadow {
  box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
}
</style>
