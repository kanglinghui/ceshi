<template>
    <div class="plgintions">
        <el-pagination
            @size-change="handleSizeChange"
            @current-change="handleCurrentChange"
            :current-page.sync="currentPage"
            :pager-count="5"
            :page-size="size"
            layout="prev, pager, next, jumper"
            :total="total">
        </el-pagination>
    </div>
</template>
<script>
export default {
    name:'pagin',
    props:{
        size:{
            type:Number,
            default:10,
        },
        total:{
            type:Number,
            default:1000
        },
        user:{
            type:String
        }
    },
    data(){
        return {
            val:1,
            currentPage:1
        }
    },
    methods:{
        handleSizeChange(val){
            console.log(12,val);
        },
        handleCurrentChange(val){
            this.val = val;
            let obj = {};
            obj.val = val;
            obj.size = this.size;
            obj.user = this.user;
            this.$emit('changePage',obj);
        }
    }
}
</script>
<style lang="scss" scoped>
    .plgintions{
        padding:5px 0;
    }
</style>