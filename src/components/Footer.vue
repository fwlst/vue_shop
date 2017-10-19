<template>
    <section class="footer">
        Copyright © 2017 小米科技
        <!--<div class="footer__wrap">
            <div class="footer__secondary">
                <div class="footer__inner">
                    <div class="footer__region">
                        <span>区域</span>
                        <select class="footer__region__select">
                            <option value="en-US">USA</option>
                            <option value="zh-CN">中国</option>
                        </select>
                    </div>
                    <div class="footer__secondary__nav">
                        <span>Copyright © 2017 小米科技.</span>
                        <a href="#">
                            About Us
                        </a>
                        <a href="#">
                            Terms &amp; Conditions
                        </a>
                        <a href="#">
                            Privacy Policy
                        </a>
                    </div>
                </div>
            </div>
        </div>-->
    </section>
</template>

<script>
    export default {
        name: 'footer',
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
.footer{
    background-color: #f5f7fc;
    width: 100%;
    height: 50px;
    line-height: 50px;
    position: fixed;
    bottom: 0;
    text-align: center;
    font-size: 14px;
    color: #333;
}
</style>
