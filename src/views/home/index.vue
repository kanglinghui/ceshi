<template>
    <div class="home">
        <div class="box">
            <div v-for="(item,i) in list" :key="i" class="main" @click="click(i)">
                <div class="img"></div>
                <div class="text">
                    <h3>{{item.title}}</h3>
                    <div style="width:20px;height:2px;background-color:#9EA2A3"></div>
                    <p>{{item.text}}</p>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    data(){
        return{
            list:[
                {title:'查询分析',text:'Budget Monitoring'},
                {title:'预警监督',text:'Supervision and Warning sssssss'},
                {title:'信息披露',text:'Financial Enquiry'},
            ]
        }
    },
    methods:{
        click(idx){
            switch(idx){
                case 0:
                    alert(1);
                    break;
                case 1:
                    this.$router.push('/warning/index');
                    break;
                case 2:
                    alert(3);
                    break;        
            }
        }
    }
}
</script>
<style lang="scss" scoped>
@import '@/styles/variables.scss';
    .home{
        padding:10px;
        .box{
            min-width:800px;
            display: flex;
            justify-content: center;
            .main{
                &:first-child{
                    margin-left:0;
                }
                cursor: pointer;
                margin-left:20px;
                width:32%;
                height:200px;
                padding:0 8px;
                background-color:#fff;
                box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.1);
                border-radius:8px;
                display: flex;
                justify-content: center;
                overflow: hidden;
                transition: .5s;
                &:hover{
                    box-shadow:0 2px 12px 0 rgba(0, 0, 0, 0.3) ;
                }
                .img{
                    flex-shrink: 0;
                    width:120px;
                    height:120px;
                    border-radius:50%;
                    background-color: #ccc;
                    position:relative;
                    top:50%;
                    transform: translateY(-50%);
                }
                .text{
                    margin-left:10px;
                    height:120px;
                    position:relative;
                    top:50%;
                    transform: translateY(-50%);
                    h3{
                        font-size:26px;
                        color:#47545f;
                        margin:0;
                        line-height: 58px;
                    }
                    p{
                        color:#a8b0b7;
                        font-size:18px;
                        line-height:36px;
                    }
                }
            }
        }
    }
</style>