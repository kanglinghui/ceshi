<template>
    <div :id="id" :class="className" :style="{ height: height, width: width }" />
</template>
<script>
import echarts from "echarts";
import resize from "./mixins/resize";
export default {
    mixins: [resize],
    props: {
        className: {
        type: String,
        default: "chart"
        },
        id: {
        type: String,
        default: "chart"
        },
        width: {
        type: String,
        default: "200px"
        },
        height: {
        type: String,
        default: "200px"
        }
    },
    data() {
        return {
        chart: null
        };
    },
    mounted() {
        this.initChart();
    },
    beforeDestroy() {
        if (!this.chart) {
        return;
        }
        this.chart.dispose();
        this.chart = null;
    },
    methods:{
        initChart(){
            this.chart = echarts.init(document.getElementById(this.id));
            this.chart.setOption({
                tooltip: {
                    trigger: 'item',
                    formatter: '{a} <br/>{b}: {c} ({d}%)'
                },
                legend: {
                    orient: 'vertical',
                    left: 0,
                    data: ['警示指标','提示指标','备选指标']
                },
                series: [
                    {
                        name: '预警指标库',
                        type: 'pie',
                        radius: ['40%', '55%'],
                        label: {
                            formatter: '{a|{a}}{abg|}\n{hr|}\n  {b|数量:{c}}\n  {per|占比:{d}%}',
                            position: 'outer',
                            alignTo: 'labelLine',
                            bleedMargin: 50,
                            borderWidth: 1,
                            borderRadius: 4,
                            rich: {
                                a: {
                                    fontSize:10,
                                    color:'rgba(255,255,255,0)',
                                    lineHeight: 0,
                                    align: 'center'
                                },
                                hr: {
                                    width: '100%',
                                    height: 0
                                },
                                b: {
                                    fontSize:10,
                                    lineHeight: 33
                                },
                                per: {
                                    fontSize:10,
                                    padding: [2, -2],
                                }
                            }
                        },
                        labelLine:{
                            length:13,
                            length2:5
                        },
                        data: [
                            {value: 335, name: '警示指标',itemStyle:{color:'#f58250'}},
                            {value: 310, name: '提示指标',itemStyle:{color:'#21b696'}},
                            {value: 234, name: '备选指标',itemStyle:{color:'#2384ca'}},
                        ]
                    }
                ]
            })
        }
    }
}
</script>    