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
  		<div v-if="seller.supports" class="support-count" v-on:click="showInfoPage">
  			<span class="count">{{seller.supports.length}}个 </span>
  			<i> ></i>
  		</div>
  	</div>
  	<div class="bulletin-wrap" v-on:click="showInfoPage">
  		<span class="bulletin-title"></span><span class="bulletin-text">{{seller.bulletin}}</span>
  		<i> ></i>
  	</div>
  	<div class="background">
  		<img :src="seller.avatar" width="100%" height="100%">
  	</div>
  	<transition name="fade">
	  	<div v-show="infopageShow" class="infopage">
	  		<div class="infopage-wrap clearfix">
	  			<div class="infopage-main">
	  				<h1 class="name">{{seller.name}}</h1>
	  				<div class="star-wrap">
	  					<star :size="48" :score="seller.score"></star>
	  				</div>
	  				<div class="title">
	  					<div class="line"></div>
	  					<div class="text">优惠信息</div>
	  					<div class="line"></div>
	  				</div>
	  				<ul v-if="seller.supports" class="supports-list">
	  					<li v-for="item in seller.supports" class="support-item">
	  						<span class="icon" :class="classMap[item.type]"></span>
	  						<span class="text">{{item.description}}</span>
	  					</li>
	  				</ul>
	  				<div class="title">
	  					<div class="line"></div>
	  					<div class="text">商家公告</div>
	  					<div class="line"></div>
	  				</div>
	  				<div class="bulletin">
	  					<p class="content">{{seller.bulletin}}</p>
	  				</div>
	  			</div>
	  		</div>
	  		<div class="infopage-close">
	  			<i v-on:click="closeInfoPage">x</i>
	  		</div>
	  	</div>
	  </transition>
  </div>
</template>

<script>
	import star from '@/components/star/star.vue'
	export default {
		props : {
			seller : {
				type : Object
			}
		},
		data () {
			return {
				infopageShow : false
			}
		},
		methods : {
			showInfoPage : function () {
				this.infopageShow = true
			},
			closeInfoPage : function () {
				this.infopageShow = false
			}
		},
		created () {
			this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee']
		},
		components : {
			star : star
		}
	}
</script>

<style lang="stylus" rel="stylesheet/stylus">
	@import "../../common/stylus/mixin.styl"

	.header
		position: relative
		color: #fff
		overflow: hidden
		background-color: rgba(7,17,27,0.4)
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
				vertical-align: top
				margin-top: 8px
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
				top: 1px
				font-size: 10px
		.background
			position: absolute
			top: 0
			left: 0
			width: 100%
			height: 100%
			z-index: -1
			filter: blur(10px)
		.infopage
			position: fixed
			top: 0
			left: 0
			z-index: 100
			width: 100%
			height: 100%
			overflow: auto
			transition: all 2s
			background: rgba(7,17,27,0.8)
			&.fade-enter-active, &.fade-leave-active
				transition: opacity 1
			&.fade-enter-to, &.fade-leave-to
				transition: opacity 1
				
			.infopage-wrap
				width: 100%
				min-height: 100%
				.infopage-main
					margin-top: 64px
					padding-bottom: 64px
					.name
						line-height: 16px
						text-align: center
						font-size: 16px
						font-weight: bold
					.star-wrap
						margin-top: 18px
						padding: 2px 0
						text-align: center
					.title
						display: flex
						width: 80%
						margin: 30px auto 24px auto
						.line
							flex: 1
							position: relative
							top: -6px
							border-bottom: 1px solid rgba(255,255,255,0.2)
						.text
							padding: 0 12px
							font-weight: 700
							font-size: 14px
					.supports-list
						width: 80%
						margin: 0 auto
						.support-item
							padding: 0 12px
							margin-bottom: 12px
							font-size: 0
							&:last-child
								margin-bottom: 0
							.icon
								display: inline-block
								width: 16px
								height: 16px
								vertical-align: top
								margin-right: 16px
								background-size: 16px 
								background-repeat: no-repeat
								&.decrease
									bg-image("./img/decrease_2")
								&.discount
									bg-image("./img/discount_2")
								&.guarantee
									bg-image("./img/guarantee_2")
								&.invoice
									bg-image("./img/invoice_2")
								&.special
									bg-image("./img/special_2")
							.text
								line-height: 16px
								font-size: 12px
					.bulletin
						width: 80%
						margin: 0 auto
						.content
							padding: 0 12px
							line-height: 24px
							font-size: 12px
			.infopage-close
				width: 32px
				height: 32px
				margin: -64px auto
				clear: both
				color: orange
				font-size: 26px

</style>
