<template>
    <section class="container">
        <div class="test">Hello {{title}}</div>
        <div v-for="(index,key) in query" :key="key">{{key}}---{{index}}</div>
        <div v-for="(index,key) in arr" :key="index">{{key}}---{{index}}</div>
        <div v-on:click="isclick">{{name}}</div>
        <i class="iconfont">&#xe65d;</i>
    </section>
</template>

<script>
export default {
    name: 'index',
    head: {
        title: '首页'
    },
    asyncData(content) {
        //console.log(http);
        return {
            title: 'World',
            arr: [12,22,32,42,52],
            query: content.query
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
<style lang='less'>
 @import "~assets/less/common.less";
.test{
    font-size: 32*@rem;
    color: @color;
}
</style>
