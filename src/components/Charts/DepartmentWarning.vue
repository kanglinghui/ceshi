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
                trigger: 'axis',
                axisPointer: {            // 坐标轴指示器，坐标轴触发有效
                    type: 'shadow'        // 默认为直线，可选为：'line' | 'shadow'
                }
            },
            legend: {
                data: ['红色预警', '黄色预警']
            },
            grid: {
                left: '3%',
                right: '4%',
                bottom: '3%',
                containLabel: true
            },
            xAxis: [
                {
                    type: 'category',
                    data: ['外语教学部', '文理教学部', '基础医学院', '健康信息技术与管理学院', '药学院', '体育教学部', '附属卫生学校','继续教育学校','马克思主义学院','康复学院']
                }
            ],
            yAxis: [
                {
                    type: 'value'
                }
            ],
            series: [
                {
                    name: '红色预警',
                    type: 'bar',
                    stack: '预警',
                    color:'#f46665',
                    data: [75, 57, 21, 23, 21, 25, 19, 11, 5, 3]
                },
                {
                    name: '黄色预警',
                    type: 'bar',
                    stack: '预警',
                    color:'#efaf58',
                    data: [48, 40, 46, 28, 26, 18, 18, 18, 10, 6]
                }  
            ]
        })
        this.chart.on('click', (params) => {
            console.log(params.name); 
            // let obj = {};
            // obj.name = params.name;
            // this.$emit('DepartmentWarning',obj)
            this.$router.push(`/warning/WarningSummary?name=${params.name}&id=1`);
        })
      }
  }
}
</script>