<template>
    <section class="bread">
        <div class="bread-wrap">
            <nav class="">
                <a href="/">首页</a>
                <slot></slot>
            </nav>
        </div>
    </section>
</template>

<script>
    export default {
        name: '',
        data() {
            return {}
        },
        mounted() {
            // 代替ready
        },
        methods: {},
        components: {}
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style rel="stylesheet/less" lang="less" scoped>
    .bread{
        height: 45px;
        line-height: 45px;
        background-color: #f0f0f0;
        .bread-wrap{
            padding: 0 10px;
            font-size: 14px;
            color: #a1a1a1;
            a{
                position: relative;
                margin-right: 20px;
                &:after{
                    position: absolute;
                    top: -2px;
                    margin: 0 10px;
                    content:'/';
                    height:20px;
                    line-height: 20px;
                }
            }
            span{
                color:#d1434a;
            }
        }
    }


</style>
