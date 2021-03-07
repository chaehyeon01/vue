<template>
  <div class="inputBox shadow">
      <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo"> 
      <!-- <button v-on:click="addTodo">add</button> -->
      <span class="addContainer" v-on:click="addTodo" >
        <i class="fas fa-plus addBtn"></i>
      </span>
       <Modal v-if="showModal" @close="showModal = false">
        <!--
      you can use custom content here to overwrite
      default content
    -->
        <h3 slot="header"><span>경고!</span><i class="fas fa-times modalCloseTop" @click="showModal = false"></i></h3>
        <div slot="body">
          <span>내용을 입력해주세요!</span>
        </div>
        <div slot="footer">
          <p>&copy; NamChae</p>
          <span class="modal_close" @click="showModal = false">OK</span>
        </div>
      </Modal>
  </div>
</template>

<script>
import Modal from './common/Modal.vue';
export default {
  data: function() {
    return{
      newTodoItem:"",
       showModal: false
    }
  },
  methods: {
    addTodo: function(){
      if(this.newTodoItem !== ''){
        this.$emit('addTodoItem',this.newTodoItem);
        this.clearInput();
      }else{
        //모달 부분
        this.showModal= !this.showModal;
      }
     
    },
    clearInput : function(){
        this.newTodoItem='';
    }
  },
  components :{   
    Modal:Modal
  }
}
</script>

<style scoped>
input:focus {
  outline:none;
}
.inputBox {
  
  background: white;
  height:50px;
  line-height: 50px;
  border-radius: 5px;
}
.inputBox input{
  border-style:none;
  font-size: 0.9rem;
}
.addContainer {
  float:right;
  background: linear-gradient(to right,#6478FB,#8763FB);
  display: block;
  width:3rem;
  border-radius: 0 5px 5px 0;
}
.addBtn {
  color:white;
  vertical-align: middle;
}
.modalCloseTop {
  float: right;
}
.modal_close {
  display: block;
  background: linear-gradient(to right,#6478FB,#8763FB);
  border-radius:5px;
  cursor: pointer;
  width:100%;
  height:40px;
  line-height: 40px;
  color:white;
  box-shadow: 5px 5px 5px rgba(0, 0, 0, 0.1);
}
</style>