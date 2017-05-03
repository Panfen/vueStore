<template>
  <div>
    <v-header :seller="seller"></v-header>
    <div class="tab border-bottom-1px">
      <div class="tab-item">
        <router-link to="/goods">商品</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/ratings">评价</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/seller">商家</router-link>
      </div>
    </div>
    <router-view></router-view>
    <div class="content">
      I am a content
    </div>
  </div>
</template>

<script>
  import header from './components/header/header.vue'

  const ERR_OK = 0

  export default {
    data () {
      return {
        seller: {}
      }
    },
    created () {
      console.log(ERR_OK)
      /*
      this.$http.get('/api/seller').then(response => {
        var res = response.body
        if (res.errno === ERR_OK) {
          this.seller = res.data
          console.log('hhh')
          console.log(res.data.name)
        }
      })
      */
    },
    components: {
      'v-header': header
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import './common/stylus/mixin.styl'
  .tab
    display: flex
    width: 100%
    height: 40px
    line-height: 40px
    border-1px(rgba(7, 17, 27, 0.1))
    .tab-item
      flex: 1
      text-align: center
      & > a
        display: block
        font-size: 14px
        color: rgb(77, 85, 93)
        &.router-link-active
          color: rgb(240, 20, 20)

</style>
