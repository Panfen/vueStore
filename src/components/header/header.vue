<template>
  <div class="header">
  	<div class="content-wrap">
  		<div class="avatar">
  			<img :src="seller.avatar" width="64" height="64">
  		</div>
  		<div class="content"></div>
  	</div>
  	<div class="notice-wrap">
  		<div class="title">
  			<span class="brand"></span>
  			<span class="name">{{seller.name}}</span>
  		</div>
  		<div class="description">
  			{{seller.description}}/{{seller.deliveryTime}}分钟送达
  		</div>
  		<div class="supports" v-if="seller.supports">
  			<span class="icon"></span>
  			<span class="text">{{seller.supports[0].description}}</span>
  		</div>
  	</div>
  </div>
</template>

<script>
	export default {
		props : {
			seller : {
				type : Object
			}
		}
	}
</script>

<style lang="stylus" rel="stylesheet/stylus">
.header
	color: #fff
	background: #333
	.content-wrap
		padding: 24px 12px 28px 24px
		.avatar
			display: inline-block
		.content
			display: inline-block
</style>
