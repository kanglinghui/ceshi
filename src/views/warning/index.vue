<template>
    <div class="warning">
        <div class="head">
            <div v-for="(item,i) in headList" :key="i" :class="'msg' + i" class="msg" @click="LinkClick(i)">
                <div class="img"></div>
                <div class="txt">
                    <p>{{item.txt}}</p>
                    <span>{{item.num}}个</span>
                </div>
                <div>
                    <i class="el-icon-arrow-right" style="line-height:160px;"></i>
                </div>
            </div>
        </div>
        <ChartMain title="指标预警结果汇总" icon="1" click="0">
            <WarningChart height="100%" width="100%" />
        </ChartMain>
        <ChartMain title="部门预警前十结果汇总图" icon="1" click="1">
            <DepartmentWarning height="100%" width="100%" id="Department"/>
        </ChartMain>
        <ChartMain title="预警指标库" icon="2" click="2" padding="5">
            <div class="content">
                <div class="left">
                    <EarlyWarning height="100%" width="100%" id="EarlyWarning" />
                </div>
                <div class="right">
                    <el-table
                        :data="data"
                        border
                        :height="265"
                        style="width: 100%">
                        <el-table-column
                            align="center"
                            type="index"
                            label="序号"
                            width="50">
                        </el-table-column>
                        <el-table-column
                            align="center"
                            prop="type"
                            label="预警类型"
                            width="180">
                        </el-table-column>
                        <el-table-column
                            align="center"
                            prop="rules"
                            show-overflow-tooltip
                            label="预警规则">
                        </el-table-column>
                        <el-table-column
                            align="center"
                            show-overflow-tooltip
                            prop="standard"
                            label="预警标准">
                        </el-table-column>
                    </el-table>
                    <div class="pagins">
                        <Pagin :total="tableData.length" user="warning" :size="5" @changePage="change_page($event)" />
                    </div>
                </div>
            </div>
        </ChartMain>
    </div>
</template>
<script>
import WarningChart from "@/components/Charts/WarningChart";
import DepartmentWarning from "@/components/Charts/DepartmentWarning";
import EarlyWarning from "@/components/Charts/EarlyWarning";
import ChartMain from "./componetns/ChartMain";
import Pagin from "@/components/Pagin";
export default {
    components:{
        WarningChart,
        DepartmentWarning,
        EarlyWarning,
        ChartMain,
        Pagin
    },
    data(){
        return {
            headList:[
                {txt:'红色预警',num:1128},
                {txt:'黄色预警',num:68},
                {txt:'提示',num:28},
            ],
            tableData:[
                {type:'警示类',rules:'劳务费支出占比',standard:'50%一级预警，30%二级预警'},
                {type:'警示类',rules:'劳务费支出占比',standard:'50%一级预警，30%二级预警'},
                {type:'警示类',rules:'劳务费支出占比',standard:'50%一级预警，30%二级预警'},
                {type:'警示类',rules:'劳务费支出占比',standard:'50%一级预警，30%二级预警'},
                {type:'警示类',rules:'劳务费支出占比',standard:'50%一级预警，30%二级预警'},
                {type:'警示类',rules:'劳务费支出占比',standard:'50%一级预警，30%二级预警'},
                {type:'警示类',rules:'劳务费支出占比',standard:'50%一级预警，30%二级预警'},
                {type:'警示类',rules:'劳务费支出占比',standard:'50%一级预警，30%二级预警'},
            ],
            data:[],
        }
    },
    mounted(){
        this.data = this.tableData.slice(0,5);
        console.log(this.data)
    },
    methods:{
        LinkClick(idx){
            switch(idx){
                case 0:
                    alert(1);
                    break;
                case 1:
                    alert(2);
                    break;
                case 2:
                    alert(3);
                    break;        
            }
        },
        change_page(e){
            if(e.user == 'warning'){
                let { val,size } = e;
                this.data = this.tableData.slice((val-1) * size,val * size);  
            }
        }
    }
}
</script>
<style lang="scss" scoped>
    .warning{
        padding:0 20px;
        .head{
            padding:10px 0;
            display: flex;
            justify-content: space-between;
            min-width:800px;
            margin-bottom:20px;
            .msg{
                height:160px;
                width:32%;
                min-width: 260px;
                overflow: hidden;
                cursor: pointer;
                &:first-child{
                    margin-left:0;
                }
                border-radius: 8px;
                // margin-left:20px;
                color:#fff;
                padding:0 12px;
                display: flex;
                justify-content: space-between;
                transition:.5s;
                &:hover{
                    box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.5);
                }
                p{
                    font-size:20px;
                    margin:0;
                    line-height:40px;
                }
                span{
                    font-weight: 600;
                    font-size:34px;
                }
                .img{
                    flex-shrink: 0;
                    width:100px;
                    height:100px;
                    border-radius: 50%;
                    background-color: #ccc;
                    position: relative;
                    top:50%;
                    transform: translateY(-50%);
                }
                .txt{
                    height:100px;
                    position: relative;
                    margin:0 8px;
                    top:50%;
                    transform: translateY(-50%);
                }
            }
            .msg0{
                background-color: #F46665;
            }
            .msg1{
                background-color: #edaf57;
            }
            .msg2{
                background-color: #28b99a;
            }
        }
        .content{
            width:100%;
            height:490px;
            display: flex;
            flex-direction: row;
            .left{
                width:40%;
            }
            .right{
                border-left:1px solid #e7e7e7;
                padding:10px;
                width:60%;
                .pagins{
                    padding-top:20px;
                }
            }
        }
    }
</style>