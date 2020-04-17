<template>
    <div class="WarningSummary">
        <div class="header">
            <!-- <el-tabs type="border-card" v-model="tab_state" @tab-click="tab">
                <el-tab-pane label="指标预警结果汇总">
                    <Summary :tableData="tableData" :inputData="inputData" />
                </el-tab-pane>
                <el-tab-pane label="部门预警结果汇总">
                    <Summary :tableData="tableDatas" :inputData="inputDatas" />
                </el-tab-pane>
            </el-tabs> -->
            <Tabs :label="label" @tab="tabs">
                <Summary :tableData="tableData" :inputData="inputData" v-if="tab_state"/>
                <DepartentalWarningSummary :tableData="tableDatas" :inputData="inputDatas" v-else/>
            </Tabs>
        </div>
    </div>
</template>
<script>
import Summary from "./componetns/Summary";
import DepartentalWarningSummary from "./componetns/DepartmentalWarningSummary";
import Tabs from "./componetns/Tabs";
export default {
    components:{
        Summary,
        DepartentalWarningSummary,
        Tabs
    },
    data(){
        return {
            tab_state:true,
            label:[
                { label:'指标预警结果汇总' },
                { label:'部门预警结果汇总' }
            ],
            tableData:[
                {type:'部门总预算执行率',red:9,red_day:25,yellow:22,yellow_day:28 },
                {type:'三公经费',red:9,red_day:25,yellow:22,yellow_day:28 },
                {type:'项目预算执行率',red:9,red_day:25,yellow:22,yellow_day:28 },
                {type:'资产使用率',red:9,red_day:25,yellow:22,yellow_day:28 },
                {type:'项目超过执行期入账未全部完成',red:9,red_day:25,yellow:22,yellow_day:28 },
                {type:'劳务费支出占比过高',red:9,red_day:25,yellow:22,yellow_day:28 },
                {type:'项目来款单位与项目委托单位不一致',red:9,red_day:25,yellow:22,yellow_day:28 },
                {type:'无合同项目合同金额超限',red:9,red_day:25,yellow:22,yellow_day:28 },
            ],
            tableDatas:[
                {type:'外语教学部',red:10,red_day:26,yellow:23,yellow_day:29 ,sum:50},
                {type:'文理教学部',red:10,red_day:26,yellow:27,yellow_day:28,sum:50 },
                {type:'基础医学院',red:9,red_day:25,yellow:22,yellow_day:28,sum:50 },
                {type:'健康信息技术与管理学院',red:9,red_day:25,yellow:22,yellow_day:28,sum:50 },
                {type:'药学院',red:9,red_day:25,yellow:22,yellow_day:28,sum:50 },
                {type:'体育教学部',red:9,red_day:25,yellow:22,yellow_day:28,sum:50 },
                {type:'附属卫生学校',red:9,red_day:25,yellow:22,yellow_day:28,sum:50 },
                {type:'继续教育学院',red:9,red_day:25,yellow:22,yellow_day:28,sum:50 },
            ],
            inputData:[
                { value: '康凌辉' },
                { value: '龚凯迪' },
                { value: '郭帅' },
            ],
            inputDatas:[
                { value: '卡哇伊' },
                { value: '小可爱' },
                { value: '大宝宝' },
            ]
        }
    },
    methods:{
        tabs(e){
            if(e.state == 0){
                this.tab_state = true;
            }else{
               this.tab_state = false;
            }

        }
    }
}
</script>
<style lang="scss" scoped>
    .WarningSummary{
        .header{
            padding:20px;
        }
    }
</style>