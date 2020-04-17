<template>
    <div class="HeaderSet">
        <svg-icon
            class-name="set-icon"
            icon-class="set"
            @click.stop="click"
        />
    </div>
</template>
<script>
export default {
    methods:{
        click(){
            console.log('设置')
        }
    }
}
</script>
<style lang="scss" scoped>
    .HeaderSet{
        font-size: 0 !important;
        .set-icon{
            cursor: pointer;
            font-size: 18px;
            vertical-align: middle;
        }
    }
</style>