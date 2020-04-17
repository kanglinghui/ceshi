<template>
    <div class="HeaderHome">
        <svg-icon
            class-name="home-icon"
            icon-class="home"
            @click.stop="click"
        />
    </div>
</template>
<script>
export default {
    methods:{
        click(){
            this.$router.push("/home")
        }
    }
}
</script>
<style lang="scss" scoped>
    .HeaderHome{
        font-size: 0 !important;
        .home-icon{
            cursor: pointer;
            font-size: 18px;
            vertical-align: middle;
        }
    }
</style>