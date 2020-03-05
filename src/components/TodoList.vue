<template>
    <el-row>
        <el-col :xs="24" :sm="18" :md="14" :lg="8" id="main">
            <h1>TodoList</h1>
            <el-input placeholder="请输入待办事项" v-model="todo.things"></el-input>
            <el-date-picker placeholder="选择日期" v-model="todo.date" type="date" format="yyyy-MM-dd" value-format="yyyy-MM-dd" 
            @click="date"></el-date-picker>
            <el-button class="btn-add" @click="add">增加</el-button>
            <el-divider></el-divider>
            <p>进行中：{{todolist.length}}&nbsp;&nbsp;&nbsp;已完成：{{donenum}}</p>
            <el-row v-for="(item,index) in todolist" :key="item.lable" class="list-row">
                <el-col :xs="2" :sm="1" :md="1" :lg="1" :xl="1" class="check" :class="{ red: !todolist[index].done, 'green': todolist[index].done }">
                    <el-checkbox size="mini" v-model="item.done"></el-checkbox>
                </el-col>
                <el-col  :xs="20" :sm="22" :md="22" :lg="10" :xl="22">
                    <input type="text" v-model="item.things" class="ipcont" :class="{done: todolist[index].done}">
                </el-col>
                <el-col  :xs="20" :sm="22" :md="22" :lg="10" :xl="22">
                    <input type="text" v-model="item.date" class="ipcont" >
                </el-col>
                <el-col :xs="2" :sm="1" :md="1" :lg="1" :xl="1" class="close">
                    <i class="el-icon-close" @click="del(index)"></i>
                </el-col>
            </el-row>
        </el-col>
    </el-row>
</template>
<script>
import Storage from '../store/store'
export default {
    name:"TodoList",
    data(){
        return{
            todo:{
                things:'',
                date:'',
                done:false
            },
            todolist:Storage.fetch(),
            pickerOptions: {
                disabledDate(time) {
                    return time.getTime() > Date.now();
                },
            },
            date(val){
                this.todo.date = val;
            }
        }
    },
    methods:{
        add(){
            if(this.todo.things){   //  
                this.todolist.push(this.todo)
                this.todo = {things:'',done:false}
            }
            
        },
        del(index){ 
            this.todolist.splice(index,1)
        },
       
    },
    computed:{
        donenum:function() {
            return this.todolist.filter(function(val) {return val.done}).length
        }
    },
    watch:{
        todolist:{
            handler(items){Storage.save(items)},
            deep:true
        }
    }
    
}
</script>
<style>
#main{
        float: none;
        margin: 0 auto;
    }
.el-input{
        width:70%;
        padding-bottom: 5px;
    }
.btn-add{
    width:50px;
    height: 40px;
    padding:5px;
    background-color: rgb(12, 131, 71);
    color: white
}
.el-table td,.el-table th{
    height:20px;
    text-align: center; 
}
 .check,.close {
      text-align: center;
      line-height: 40px;
    }
.ipcont {
      width: 70%;
      margin-top: 8px;
      border: 0;
      line-height: 24px;
      background-color: transparent;
      font-size: 16px;
      color: #756C83;
}
.el-icon-close {
      cursor: pointer;
}
.el-icon-close:hover{
    color: #ef5f65;
}
 .red {
    border-left: #ef5f65 2px solid;
}

.green {
    border-left: #B9E1DC 2px solid;
}
.done {
      text-decoration: line-through;
    }
</style>