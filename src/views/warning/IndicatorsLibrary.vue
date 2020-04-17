<template>
    <div class="IndicatorsLibrary">
        <Tabs :tableData="dataList" @tab="tabs($event)" :label="label"> 
            <div>{{txt}}</div>
        </Tabs>
    </div>
</template>
<script>
import Tabs from './componetns/Tabs';
export default {
    components:{
        Tabs
    },
    data(){
        return {
            label:[
                { label:'提示指标汇总表' },
            ],
            txt:'我是帅哥'
        }
    },
    methods:{
        tabs(e){
            console.log(e)
        }
    }
}
</script>
<style lang="scss" scoped>

</style>