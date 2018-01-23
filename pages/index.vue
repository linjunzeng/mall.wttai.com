<template>
    <section class="container">
        <div class="content" v-if="indexdata.length != 0">
            <div v-for='(item, key) in indexdata' :key="key" class="index_con">
                <div v-if="item.type_code == 9991" class="webinfo_con clearfix">
                    <div class="share_info_text fr">
                        <p>分享次数：{{item.son[0].content_share}}</p>
                        <a href="http://zs.upinkji.com">招商加盟</a>
                    </div>
                    <div class="img fl"><img :src="item.son[0].content_image"></div>
                    <div class="share_info_text_l">
                        <div class="name textover">{{item.son[0].content_title}}</div>
                        <div class="txt textover3">{{item.son[0].content_desc}}</div>
                    </div>
                </div>

                <div class="area_con" v-if="item.type_code == 2 || item.type_code == 3">
                    <div v-if="item.show_title == 1" class="title">{{item.title}}</div>
                    <ul>
                        <li :style="{width: 100/item.son.length+'%'}" v-for="(list, index) in item.son" :key="index">
                            <a :href="list.content_url">
                                <img :src="list.content_image">
                            </a>
                        </li>
                    </ul>
                </div>

                <div class="area_con area_con_1" v-if="item.type_code == 5 || item.type_code == 8">
                    <div v-if="item.show_title == 1" class="title">{{item.title}}</div>
                    <ul>
                        <li v-for="(list, index) in item.son" :key="index">
                            <a :href="list.content_url">
                                <img :src="list.content_image">
                            </a>
                        </li>
                    </ul>
                </div>

                <div class="area_con area_con_2" v-if="item.type_code == 4 || item.type_code == 6">
                    <div v-if="item.show_title == 1" class="title">{{item.title}}</div>
                    <ul>
                        <li v-for="(list, index) in item.son" :key="index">
                            <a :href="list.content_url">
                                <img :src="list.content_image">
                            </a>
                        </li>
                    </ul>
                </div>


                <div class="area_con area_con_1 area_con_3" v-if="item.type_code == 9">
                    <div v-if="item.show_title == 1" class="title">{{item.title}}</div>
                    <ul v-if="item.son.length != 0">
                        <li v-for="(list, index) in item.son" :key="index">
                            <a :href="list.content_url">
                                <div class="list_box_img">
                                    <img :src="list.content_image">
                                </div>
                                <div class="list_box_title textover2">{{list.content_title}}</div>
                                <div class="list_box_price">￥{{list.content_price_sale}} <del>￥{{list.content_price_market}}</del></div>
                            </a>
                        </li>
                    </ul>
                </div>
            </div>
        </div>
        <div v-on:click="isclick">{{name}}</div>
    </section>
</template>

<script>
import axios from '../plugins/axios'
export default {
    name: 'index',
    head: {
        title: '首页'
    },
    async asyncData(content) {
        let { data } = await axios.get('/index');
        console.log(data.data);
        return {
            indexdata: data.data
        }
    },
    data () {
        return {
            name: 'default'
        }
    },
    methods: {
        isclick: function(){
            this.name = this.name == 'change' ? 'default' : 'change';
        }
    }
}
</script>
<style  lang='less' scoped>
 @import "~assets/less/common.less";
/* 搜索框 */
a{display: block;}
img{width: 100%;}
.search_con{overflow: hidden;background: #fff;}
.search{margin: 0.2rem 0.32rem 0;padding: 0.146667rem 0;border-radius: 0.373333rem;text-align: center;background: #ebebeb;overflow: hidden;}

/* 头部信息 */
.webinfo_con .img{width:24%;height:0;position:relative;left:0;top:0.133333rem;padding-bottom:24%;display:inline-block}
.webinfo_con .img img{max-width:74%;max-height:74%;margin:auto;position:absolute;left:0;top:0;bottom:0;right:0;border:.1rem solid #ebebeb;border-radius:50%;z-index:1}

.webinfo_con .share_info_text_l{padding:0.15rem 0;overflow:hidden;}
.webinfo_con .name{width:100%;line-height:.8rem;font-size:.4rem;color:#333}
.webinfo_con .txt{line-height:.5rem;font-size:.3rem;color:#666}

.webinfo_con .share_info_text{padding-top:0.55rem;}
.webinfo_con .share_info_text p{line-height:.8rem;font-size:.3rem;color:#666}
.webinfo_con .share_info_text a{padding: 0.213rem 0.426667rem;margin-top:.3rem;background:#e41b45;font-size:0.293rem;color:#fff;border-radius:0.4rem;text-align:center}

/* 模块 */
.area_con ul li{display: inline-block;box-sizing: border-box;}
.area_con .title{margin: 0.133333rem 0 -0.133333rem;width: 100%;height: 1.2rem;line-height: 1.2rem;text-align: center;background: #fff;}

.area_con_1 ul li{margin-top: 0.133333rem;width: 50%;}
.area_con_1 li:nth-child(2n){padding-left: 0.066667rem;}
.area_con_1 li:nth-child(2n+1){padding-right: 0.066667rem;}

.area_con_2 ul{margin-top: 0.133333rem;}

.area_con_3 .title{margin: 0.133333rem 0 0;}
.area_con_3 ul li{margin-top: 0.133333rem}
.area_con_3 li a{padding: 0.133333rem;overflow:hidden;background: #fff;}
.area_con_3 li .list_box_img{padding:50% 0;width:100%;height:0;overflow:hidden;position:relative;}
.area_con_3 li .list_box_img img{margin:auto;position:absolute;top:0;left:0;right:0;bottom:0;}

.area_con_3 li .list_box_title{margin-top: 0.133rem;width: 100%;height: 1.067rem;line-height: 0.533rem;}
.area_con_3 li .list_box_price{line-height: 0.8rem;font-size: 0.373333rem;color: #e41b45;}
.area_con_3 li .list_box_price del{margin-left: 0.106667rem;font-size: 0.133333rem;color: #666;}
</style>
