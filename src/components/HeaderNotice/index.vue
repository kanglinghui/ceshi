<template>
    <div class="HeaderNotice">
        <el-badge :value="12" class="item">
            <svg-icon
                class-name="notice-icon"
                icon-class="notice"
                @click.stop="click"
            />
        </el-badge>
    </div>
</template>
<script>
export default {
    methods:{
        click(){
            console.log(notice)
        }
    }
}
</script>
<style lang="scss" scoped>
    /deep/.el-badge__content.el-badge__content--undefined.is-fixed{
        top:10px;
    }
    .HeaderNotice{
        font-size: 0 !important;
        .notice-icon{
            cursor: pointer;
            font-size: 18px;
            vertical-align: middle;
        }
    }
</style>