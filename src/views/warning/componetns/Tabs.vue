<template>
    <div class="WarningSummary">
        <div class="header">
            <el-tabs type="border-card" @tab-click="tabs" v-model="activeTab">
                <el-tab-pane v-for="(item,i) in label" :key="i" :label="item.label" :name="i + ''">
                    <slot/>
                </el-tab-pane>
            </el-tabs>
        </div>
    </div>
</template>
<script>
export default {
    props:{
        label:{
            type:Array,
        },
    },
    mounted(){
        if(this.$route.query.id){
            console.log('id',this.$route.query.id)
            this.activeTab = this.$route.query.id;
            let obj = {};
            obj.index = this.$route.query.id;
            obj.label = this.label[this.$route.query.id].label;
            console.log(obj)
            this.tabs(obj)
        }
    },
    data(){
        return {
            activeTab:'0',
            tableDatass:[
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
                {type:'部门总预算执行率',red:10,red_day:26,yellow:23,yellow_day:29 },
                {type:'三公经费',red:10,red_day:26,yellow:27,yellow_day:28 },
                {type:'项目预算执行率',red:9,red_day:25,yellow:22,yellow_day:28 },
                {type:'资产使用率',red:9,red_day:25,yellow:22,yellow_day:28 },
                {type:'项目超过执行期入账未全部完成',red:9,red_day:25,yellow:22,yellow_day:28 },
                {type:'劳务费支出占比过高',red:9,red_day:25,yellow:22,yellow_day:28 },
                {type:'项目来款单位与项目委托单位不一致',red:9,red_day:25,yellow:22,yellow_day:28 },
                {type:'无合同项目合同金额超限',red:9,red_day:25,yellow:22,yellow_day:28 },
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
            let obj = {};
            obj.state = e.index;
            obj.label = e.label;
            this.$emit('tab',obj)
            // if(e.paneName == 0){
            //     this.$emit('tabs',)
            // }
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