<template>
  <div class="header">
  	<div class="content-wrap">
  		<div class="avatar">
  			<img :src="seller.avatar" width="64" height="64">
  		</div>
  		<div class="content">
  			<div class="notice-wrap">
		  		<div class="title">
		  			<span class="brand"></span>
		  			<span class="name">{{seller.name}}</span>
		  		</div>
		  		<div class="description">
		  			{{seller.description}}/{{seller.deliveryTime}}分钟送达
		  		</div>
		  		<div class="supports" v-if="seller.supports">
		  			<span class="icon" :class="classMap[seller.supports[0].type]"></span>
		  			<span class="text">{{seller.supports[0].description}}</span>
		  		</div>
		  	</div>
  		</div>
  		<div v-if="seller.supports" class="support-count">
  			<span class="count">{{seller.supports.length}}个 </span>
  			<i> ></i>
  		</div>
  	</div>
  	<div class="bulletin-wrap">
  		<span class="bulletin-title"></span><span class="bulletin-text">{{seller.bulletin}}</span>
  		<i> ></i>
  	</div>
  </div>
</template>

<script>
	export default {
		props : {
			seller : {
				type : Object
			}
		},
		created () {
			this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee']
		}
	}
</script>

<style lang="stylus" rel="stylesheet/stylus">
	@import "../../common/stylus/mixin.styl"

	.header
		color: #fff
		background: #333
		.content-wrap
			padding: 24px 12px 28px 24px
			position: relative
			font-size: 0
			.avatar
				display: inline-block
				vertical-align: top
				img
					border-radius: 2px
			.content
				display: inline-block
				font-size: 14px
				margin-left: 16px
				.title
					margin-bottom: 12px
					.brand
						display: inline-block
						vertical-align: top
						width: 30px
						height: 18px
						bg-image("./img/brand")
						background-size: 30px 18px
						background-repeat: no-repeat
					.name
						margin-left: 6px
						font-size: 16px
						line-height: 18px
						font-weight: bold
				.description
					margin-bottom: 10px
					line-height: 12px
					font-size: 12px
				.supports
					.icon
						display: inline-block
						vertical-align:	top
						width: 12px
						height: 12px
						margin-right: 4px
						background-size: 12px 12px
						background-repeat: no-repeat
						&.decrease
							bg-image("./img/decrease_1")
						&.discount
							bg-image("./img/discount_1")
						&.guarantee
							bg-image("./img/guarantee_1")
						&.invoice
							bg-image("./img/invoice_1")
						&.special
							bg-image("./img/special_1")
					.text
						line-height: 12px
						font-size: 10px
			.support-count
				width: 60px
				height: 38px
				line-height: 38px
				background: rgba(0,0,0,0.2)
				position: absolute
				bottom: 28px
				right: 10px
				border-radius: 24px
				text-align: center
				.count
					color: #ccc
					font-size: 12px
				i
					color: #ccc
					font-size: 12px
		.bulletin-wrap
			height: 28px
			line-height: 28px
			padding: 0 22px 0 12px
			white-space: nowrap
			overflow: hidden
			text-overflow: ellipsis
			position: relative
			background: rgba(7,17,27,0.2)
			.bulletin-title
				display: inline-block
				width: 22px
				height: 12px
				bg-image("./img/bulletin")
				background-size: 22px 12px
			.bulletin-text
				vertical-align: top
				margin: 0 4px
				font-size: 10px
			i
				position: absolute
				right: 12px
				top: 0px
				font-size: 10px

</style>
