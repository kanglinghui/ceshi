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
          this.chart.setOption(
              {
                tooltip: {
                    trigger: 'axis'
                },
                legend: {
                    data: ['黄色预警', '红色预警']
                },
                toolbox: {
                    show: true,
                    feature: {
                        dataView: {show: false, readOnly: false},
                        magicType: {show: false, type: ['line', 'bar']},
                        restore: {show: false},
                        saveAsImage: {show: false}
                    }
                },
                // calculable: true,
                xAxis: [
                    {
                        axisLabel:{
                            interval:0,
                            rich:{
                                width:'5px'
                            },
                            formatter:function(value){
                                let valueText = '';
                                if(value.length>5){
                                    valueText = value.substring(0,5) + '...';
                                }else{
                                    valueText = value;
                                }
                                console.log(123)
                                return valueText;
                            }
                        },
                        type: 'category',
                        data: ['部门总预算执行率', '三公经费', '项目预算执行', '资产使用率', '项目超过执行期入账未全部完成', '劳务费支出占比过高', '项目来款单位与项目委托单位不一致', '无合同项目合同金额超限', '资金流向预警', '大额支出预警', '项目支出金额高比例支出至同一单位']
                    }
                ],
                yAxis: [
                    {
                        type: 'value'
                    }
                ],
                series: [
                    {
                        name: '黄色预警',
                        type: 'bar',
                        color: '#efaf58',
                        data: [11, 7, 9,27, 27, 71, 175, 179, 49, 19, 9]
                    },
                    {
                        name: '红色预警',
                        type: 'bar',
                        color: '#f46665',
                        data: [8, 6, 12, 22, 26, 76, 136, 162, 32, 20, 6]
                    }
                ]
            }
          )
          this.chart.on('click', function(params) {
            console.log(params.name); 
            // var name = parseInt(params.name);
          })
      }
  }
}
</script>