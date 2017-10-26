<template>
    <section class="good_list">
        <nav-header></nav-header>
        <nav-bread>
            <span>goods</span>
        </nav-bread>


        <section class="main">
            <div class="filter-nav">
                <span class="sortby">排序:</span>
                <a href="javascript:void(0)" class="default cur">默认</a>
                <a href="javascript:void(0)" class="price sort-up" @click="priceSort">价格
                    <svg class="icon icon-arrow-short" id="icon-arrow-short" viewBox="0 0 25 32" width="100%" height="100%"><title>arrow-short</title>
                        <path d="M24.487 18.922l-1.948-1.948-8.904 8.904v-25.878h-2.783v25.878l-8.904-8.904-1.948 1.948 12.243 12.243z" class="path1"></path>
                    </svg>
                </a>
            </div>
            <div class="good_list_wrap">
                <div class="good_nav">
                    <dl class="filter-price">
                        <dt>价格:</dt>
                        <dd><a href="javascript:void(0)" @click="setPriceFilter('all')"
                               :class="{'cur':priceChecked=='all'}">所有</a></dd>
                        <dd v-for="(item,index) in priceFilter">
                            <a href="javascript:void(0)" @click="setPriceFilter(index)"
                               :class="{'cur':priceChecked==index}">{{item.startPrice}} - {{item.endPrice}}</a>
                        </dd>
                    </dl>
                </div>
                <ul class="good_list_ul">
                    <li class="list_item" v-for="(item,index) in goodList" :key="index">
                        <div class="pic">
                            <img v-lazy="'static/img/'+item.productImg"/>
                        </div>
                        <div class="good_info">
                            <div class="name">{{item.productName}}</div>
                            <div class="price">{{item.productPrice}}</div>
                            <div class="btn_area" @click="addCart(item.productId)">加入购物车</div>
                        </div>
                    </li>
                </ul>
            </div>
        </section>


        <nav-footer></nav-footer>
    </section>
</template>

<script>
    import navHeader from '@/components/Header'
    import navFooter from '@/components/Footer'
    import navBread from '@/components/Bread'
    import axios from 'axios'

    export default {
        name: 'GoodList',
        data() {
            return {
                goodList: [],
                priceFilter: [
                    {
                        startPrice: '0.00',
                        endPrice: '100.00'
                    },
                    {
                        startPrice: '100.00',
                        endPrice: '500.00'
                    },
                    {
                        startPrice: '500.00',
                        endPrice: '1000.00'
                    },
                    {
                        startPrice: '1000.00',
                        endPrice: '5000.00'
                    }
                ],
                priceChecked: 'all',
                page: 1,
                pageSize: 8,
                sort: 1
            }
        },
        mounted() {
            // 代替ready
            this.getGoodList();
        },
        methods: {
            getGoodList() {
                let priceLevel = 'all';
                if(this.priceChecked != 'all'){
                    priceLevel = this.priceFilter[this.priceChecked];
                }
                let param = {
                    page:this.page,
                    pageSize: this.pageSize,
                    sort: this.sort,
                    priceChecked: priceLevel
                };
                axios.get('/goods', {
                    params: param
                }).then((res) => {
                    res = res.data;
                    if (res.code == 200) {
                        //let goodList = this.goodList.concat(res.data.goodList);
                        let goodList = res.data.goodList;
                        this.goodList = goodList;
                    } else {
                        console.log(res.msg);
                    }

                })
            },
            setPriceFilter(index) {
                this.priceChecked = index;
                this.page = 1;
                this.getGoodList();
            },
            priceSort(){
                this.sort = this.sort == 1 ? -1 : 1;
                console.log(this.sort);
                this.getGoodList();
            },
            addCart(productId){
                axios.post('/goods/addCart', {
                    productId: productId
                }).then((res) => {
                    res = res.data;
                    if (res.code == 200) {
                        alert(res.data);
                    } else {
                        console.log(res.msg);
                    }

                })
            }
        },
        components: {
            navHeader,
            navFooter,
            navBread
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style rel="stylesheet/less" lang="less" scoped>
    .main {
        padding-bottom: 50px;
        .filter-nav {
            height: 45px;
            line-height: 45px;
            padding: 0 20px;
            margin-bottom: 15px;
            background: #fff;
            text-align: right;
            overflow: hidden;
            font-size: 12px;
            border-bottom: 1px solid #ddd;
            .icon-arrow-short {
                width: 11px;
                height: 11px;
            }
            a {

                &.cur, &:hover {
                    color: #ee7a23;
                }
            }
        }
        .good_list_wrap {
            display: flex;
            .good_nav {
                flex: 0 0 200px;
                padding: 0 20px;
                color: #605f5f;
                transition: right .5s ease-out;
                //background-color: yellow;
                .filter-price {
                    min-height: 180px;
                    margin-bottom: 50px;
                    dt {
                        margin-bottom: 30px;
                        font-family: moderat, sans-serif;
                        letter-spacing: .25em;
                        text-transform: uppercase;
                        font-weight: 700;
                    }
                    dd {
                        line-height: 1.2em;
                        margin: 20px 0;
                        a {
                            display: block;
                            padding: 5px 0;
                            transition: padding-left .3s ease-out;
                            &.cur, &:hover {
                                color: #ee7a23;
                                transition: padding-left .3s ease-out;
                                border-left: 2px solid #ee7a23;
                                padding-left: 15px;
                            }
                        }
                    }
                }
            }
            .good_list_ul {
                width: 100%;
                .list_item {
                    float: left;
                    width: 23.10952%;
                    margin-right: 1.5873%;
                    margin-bottom: 1.5873%;
                    background: #fff;
                    border: 1px solid #e9e9e9;
                    .pic {
                        width: 100%;
                        img {
                            width: 100%;
                            display: block;
                        }
                    }
                    .good_info {
                        padding: 20px 10px 10px;
                        .name {
                            margin-bottom: 15px;
                            padding-bottom: 10px;
                            font-family: moderat, sans-serif;
                            font-weight: 700;
                            overflow: hidden;
                        }
                        .price {
                            margin-bottom: 10px;
                            line-height: 30px;
                            color: #d1434a;
                            font-size: 1.25em;
                        }
                        .btn_area {
                            width: 100%;
                            display: inline-block;
                            text-align: center;
                            font-size: 1rem;
                            font-family: moderat, sans-serif;
                            font-weight: 700;
                            border: 1px solid #d1434a;
                            color: #d1434a;
                            text-transform: uppercase;
                            letter-spacing: .25em;
                            white-space: nowrap;
                            height: 40px;
                            line-height: 40px;
                        }
                    }
                }
            }
        }
    }
</style>
