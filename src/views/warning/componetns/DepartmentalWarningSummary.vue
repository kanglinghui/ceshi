<template>
    <div class="DepartmentalWarningSummary">
        <div class="header">
            <el-autocomplete
            class="inline-input"
            style="width:50%;"
            v-model="input"
            :fetch-suggestions="querySearch"
            placeholder="请输入内容"
            :trigger-on-focus="false"
            @select="handleSelect"
            ></el-autocomplete>
            <el-button type="primary" style="background-color:#3c85c7;border-color:#3c85c7;">搜索</el-button>
            <el-button v-show="!handle" style="float:right;" @click="back">返回上一级</el-button>
        </div>
        <div class="main">
            <ul>
                <li>单位</li>
                <li>预警级别</li>
            </ul>
            <el-table
                :data="handle?tableData:tableDatas"
                :header-cell-style="getRowClass"
                border
                style="width: 100%">
                <el-table-column
                    align="center"
                    label="序号"
                    min-width="13%">
                    <template scope="scope">
                        <span v-text="scope.$index+1">{{scope.$index+1}}</span>
                    </template>
                </el-table-column>
                <el-table-column
                    align="center"  
                    label="名称"
                    show-overflow-tooltip
                    min-width="25%">
                    <template scope="scope">
                        <div class="handclick" @click="handleClick(scope.row)" v-if="handle">{{scope.row.type}}</div>
                        <div class="handclick" @click="detailClick(scope.row)" v-else>{{scope.row.type}}</div>
                    </template>
                </el-table-column>
                <el-table-column
                    align="center"
                    prop="sum"
                    label="总数"
                    show-overflow-tooltip
                    min-width="10%">
                </el-table-column>
                <el-table-column
                    align="center"
                    prop="red"
                    min-width="12.5%"
                    show-overflow-tooltip
                    label="红色预警">
                </el-table-column>
                <el-table-column
                    align="center"
                    show-overflow-tooltip
                    prop="red_day"
                    min-width="12.5%"
                    label="最大天数">
                </el-table-column>
                <el-table-column
                    align="center"
                    min-width="12.5%"
                    show-overflow-tooltip
                    prop="yellow"
                    label="黄色预警">
                </el-table-column>
                <el-table-column
                    align="center"
                    min-width="12.5%"
                    show-overflow-tooltip
                    prop="yellow_day"
                    label="最大天数">
                </el-table-column>
            </el-table>
        </div>
    </div>
</template>
<script>
export default {
    props:{
        tableData:{
            type:Array,
            default:[]
        },
        inputData:{
            type:Array,
            default:[]
        }
    },
    data(){
        return {
            input: '',
            handle:true,
            tableDatas:[],
            inputDatas:[],
        }
    },
    created(){
        console.log(this.$route.query.name)
        if(this.$route.query.name){
            this.handleClick(this.$route.query.name)
        }
    },
    mounted(){
        this._INIT();
    },
    methods:{
        _INIT(){
            // if(this.tableData.length){
            //     this.tableDatas = this.tableData;
            // }
            // if(this.inputData.length){
            //     this.inputDatas = this.inputData;
            // }
        },
        getRowClass({ row, column, rowIndex, columnIndex }) {
            if (rowIndex == 0 && columnIndex < 3) {
                return "background:#3c85c7;color:#fff";
            } else if(rowIndex == 0 && columnIndex > 2 && columnIndex < 5){
                return "background:#FEDDDB;color:#de7a74";
            } else if(rowIndex == 0 && columnIndex > 4){
                return "background:#f9ebce;color:#e29d0c";
            } else {
                return "'";
            }
        },
        back(){
            if(!this.handle){
                this.handle = true;
            }
        },
        querySearch(queryString, cb) {
            var restaurants = this.inputData;
            var results = queryString ? restaurants.filter(this.createFilter(queryString)) : restaurants;
            // 调用 callback 返回建议列表的数据
            cb(results);
        },
        createFilter(queryString) {
            return (restaurant) => {
            return (restaurant.value.toLowerCase().indexOf(queryString.toLowerCase()) === 0);
            };
        },
         handleSelect(item) {
            console.log(item);
        },
        handleClick(e){
            this.handle = false;
            console.log(e)
            this.tableDatas = [
                {type:'外语教研组',red:10,red_day:26,yellow:23,yellow_day:29 ,sum:50},
                {type:'外语办公室',red:10,red_day:26,yellow:27,yellow_day:28,sum:50 },
                {type:'外语学生办',red:9,red_day:25,yellow:22,yellow_day:28,sum:50 },
                
            ]
        },
        detailClick(e){
            console.log(e)
        }
    }
}
</script>
<style lang="scss" scoped>
    .DepartmentalWarningSummary{
        padding:10px;
        .handclick{
            cursor:pointer;
            transition: .5s;
            &:hover{
                text-decoration:underline;
                color:#3c85c7;
            }
        }
        .header{
            padding:10px;
        }
        .main{
            width:100%;
            ul{
                display: flex;
                flex-direction: row;
                padding:0;
                margin-bottom:0;
                li{
                    list-style: none;
                    text-align: center;
                    border-right:1px solid #ccc;
                    flex-shrink: 0;
                    width:50%;
                    font-size:16px;
                    line-height: 44px;
                    color:#fff;
                    background-color: #3c85c7;
                }
            }
        }
    }
</style>