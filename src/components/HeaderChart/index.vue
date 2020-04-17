<template>
    <div class="HeaderChart">
        <svg-icon
            class-name="chart-icon"
            icon-class="chart"
            @click.stop="click"
        />
    </div>
</template>
<script>
export default {
    methods:{
        click(){
            alert(1)
        }
    }
}
</script>
<style lang="scss" scoped>
    .HeaderChart{
        font-size: 0 !important;
        .chart-icon{
            cursor: pointer;
            font-size: 18px;
            vertical-align: middle;
        }
    }
</style>