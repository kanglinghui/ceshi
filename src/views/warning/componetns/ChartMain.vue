<template>
    <div class="main" >
        <div class="top_title">
            <div class="top_title_left">
                <i class="iconfont">&#xe670;</i>
                <span>{{title}}</span>
            </div>
            <div class="top_title_right" @click="btn(click)">
                <span>更多</span>
                <i class="iconfont">&#xe63c;</i>
            </div>
        </div>
        <div class="top_main">
            <slot/>
        </div>
    </div>
</template>
<script>
export default {
    props:[
        'title','icon','click','padding'
    ],
    methods:{
        btn(i){
            console.log(i)
            switch(i){
                case '0':
                    this.$router.push('/warning/WarningSummary');
                    break;
                case '1':
                    this.$router.push('/warning/IndicatorsSummary');
                    break;
                case '2':
                    this.$router.push('/warning/IndicatorsLibrary');
                    break;        
            }
        }
    }
}
</script>
<style lang="scss" scoped>
    .main{
        min-width: 800px;
        padding:0 20px;
        margin-bottom:20px;
        box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.2);
        border-radius: 10px;
        .top_title{
            display: flex;
            justify-content: space-between;
            color:#565c5f;
            font-size:20px;
            border-bottom:1px solid #e9e9e9;
            line-height:60px;
            .iconfont{
                font-size:18px;
                color:#afb0b2;
            }
            .top_title_right{
                cursor: pointer;
                transition: .5s;
                &:hover{
                    text-shadow: 2px 2px 8px #999;
                }
            }
        }
        .top_main{
            padding-top:10px;
            height:500px;
        }
    }
</style>