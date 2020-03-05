<template>
    <el-row>
        <el-col :xs="24" :sm="18" :md="14" :lg="7" id="main">
        姓名：{{info.name}}
        <el-input  placeholder="请输入姓名" v-model="info.name" maxlength="15"></el-input><br>
        年龄：{{info.age}}
        <el-input v-model="info.age" maxlength="15" placeholder="请输入年龄"></el-input><br>
        性别：{{info.sex}}
        <el-select v-model="info.sex"  placeholder="请选择">
            <el-option maxlength="20" v-for="item in options" :key="item" :value="item"></el-option>
        </el-select>
        <el-button class="btn-auto" @click="create">创建</el-button>
        <template>
            <el-table :data="tabledata" align="left">
                <el-table-column prop="name" label="姓名"></el-table-column>
                <el-table-column prop="age" label="年龄"></el-table-column>
                <el-table-column prop="sex" label="性别"></el-table-column>
                <el-table-column label="操作">
                    <template slot-scope="a">
                        <el-button size="mini" type="danger" @click="del(a.$index)">删除</el-button>
                    </template>
                </el-table-column>
            </el-table>
        </template>
        </el-col>
    </el-row>
</template>
<script>
import Storage from '../store/store'
export default{
    name: "NewContact",
    data(){
        return{
            info:{
                name:'',
                age:null,
                sex:''
            },
            options:[
                '男','女','保密'
            ],
            tabledata:Storage.fetch()
        }
    },
    methods:{
        create(){
            if(this.info.name || this.info.age || this.info.sex){
                this.tabledata.push(this.info)
                this.info = {name:'',age:null,sex:''}
            }
           
        },
        del(index){
            this.tabledata.splice(index,1)
        }
    },
    watch:{
        tabledata:{
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
        /* width:70%; */
        padding-bottom: 5px;
    }


.el-select {
        display: block;
        float: none;
    }
        
.btn-auto{
        width: 100%;
        margin-top: 12px;
        background-color: rgb(12, 131, 71);
        color: white
    }
</style>