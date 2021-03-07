<template>
  <div>
      <transition-group name="list" tag="ul">

        <li class="shadow" v-for="(todoItem,index) in propsdata" v-bind:key="todoItem.item">
          <i class="checkBtn fas fa-check" v-bind:class="{checkBtnCompleted: todoItem.completed}" v-on:click="toggleComplete(todoItem,index)"></i>
          <span v-bind:class="{textCompleted: todoItem.completed }" >{{todoItem.item}}</span>
          <span class="removeBtn" v-on:click="removeTodo(todoItem,index)">
            <i class="fas fa-trash-alt"></i>
          </span>
        </li>

      </transition-group>
  </div>
</template>

<script scoped>

export default {
  props:['propsdata'],
  methods: {
    removeTodo:function(todoItem, index){
      // console.log(todoItem+'/'+index);
      this.$emit('removeItem',todoItem,index);
      // localStorage.removeItem(todoItem);
      // this.todoItems.splice(index,1); //어떤배열에서 어떤 자리에 있는 데이터를 하나 지우겠다.
    },
    toggleComplete:function(todoItem, index){

      this.$emit('toggleItem',todoItem,index);
      //console.log(todoItem,index);
      // //로컬스트리지 데이타 갱신
      // todoItem.completed= !todoItem.completed;
      // localStorage.removeItem(todoItem.item);
      // localStorage.setItem(todoItem.item,JSON.stringify(todoItem));
    }
  }
 
  
}
</script>

<style>
ul {
  list-style-type: none;
  padding-left:0px;
  margin-top:0;
  text-align: left;
}
li {
  display: flex;
  min-height: 50px;
  height: 50px;
  line-height: 50px;
  margin:0.5rem 0;
  padding:0 0.9rem;
  background: white;
  border-radius: 5px;
}
.removeBtn {
  margin-left:auto;
  color:#de4343;
}
.checkBtn {
  line-height: 45px;
  color:#62acde;
  margin-right: 5px;
  cursor: pointer;
}
.checkBtnCompleted {
  color:#b3adad;
}
.textCompleted {
  text-decoration: line-through;
  color: #b3adad;
}
.removeBtn {
  margin-left:auto;
  color:#de4343;
  cursor: pointer;
}
/* 리스트 아이템 트렌지션 효과 */

.list-enter-active, .list-leave-active {
  transition: all 1s;
}
.list-enter, .list-leave-to /* .list-leave-active below version 2.1.8 */ {
  opacity: 0;
  transform: translateY(30px);
}
</style>