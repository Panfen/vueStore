<template>
	<div class="shopcart">
		<div class="content">
			<div class="content-left">
				<div class="logo-wrap" :class="{'exist' : totalCount > 0}">
					<div class="logo">
	          <span class="icon">
	          </span>
					</div>
					<span class="count">{{totalCount}}</span>
				</div>
				<div class="price" :class="{'exist' : totalPrice > 0}">¥ {{totalPrice}}</div>
				<div class="desc">配送费¥{{deliveryPrice}}元</div>
			</div>
			<div class="content-right" :class="{'topay' : totalPrice >= minPrice}"> {{payDesc}} </div>
		</div>
	</div>
</template>

<script type="text/javascript" src="../../common/iconfont/iconfont.js"></script>
<script>
	export default {
		props : {
			deliveryPrice : {
				type : Number,
				default : 0
			},
			minPrice : {
				type : Number,
				default : 0
			},
			selectedFoods : {
				type : Array,
				default () {
					return [
						{
							price : 10,
							count : 2
						},
						{
							price : 5,
							count : 3
						}
					]
				}
			}
		},
		computed : {
			totalPrice () {
				var total = 0
				this.selectedFoods.forEach((food) => {
					total += food.price * food.count
				})
				return total
			},
			totalCount () {
				var count = 0
				this.selectedFoods.forEach((food) => {
					count += food.count
				})
				return count
			},
			payDesc () {
				if (this.totalPrice === 0) {
					return `¥${this.minPrice}起送`
				} else if (this.totalPrice < this.minPrice) {
					return '还差¥' + (this.minPrice - this.totalPrice) + '起送'
				} else {
					return '去结算'
				}
			}
		}
	}
</script>

<style lang="stylus" rel="stylesheet/stylus">
	@import "../../common/stylus/mixin.styl"

	.shopcart
		position: fixed
		bottom: 0
		left: 0
		z-index: 50
		width: 100%
		height: 48px
		.content
			display: flex
			background: #141d27
			font-size: 0 
			.content-left
				flex: 1
				.logo-wrap
					display: inline-block
					position: relative
					top: -10px
					margin: 0 12px
					padding: 6px
					width: 56px
					height: 56px
					box-sizing: border-box
					vertical-align: top
					border-radius: 50%
					background: #141d27
					&.exist
						background: #0080D9
						.icon
							background: #0080D9
					.logo
						position: relative
						width: 100%
						height: 100%
						border-radius: 50%
						background: #2b343c
						.icon
							display: inline-block
							position: absolute
							top: 0px
							left: -2px
							vertical-align: top
							width: 50px
							height: 50px
							border-radius: 25px
							bg-image("./img/shopcart")
							background-repeat: no-repeat
							background-position: center center
					.count
						display: inline-block
						position: absolute
						top: 0px
						right: 6px
						width: 22px
						height: 14px
						border-radius: 11px
						line-height: 18px
						text-align: center
						font-size: 10px
						color: #fff;
						background: #FF2D00
				.price
					display: inline-block
					vertical-align: top
					margin-top: 12px
					line-height: 24px
					padding-right: 12px
					box-sizing: border-box
					border-right: 1px solid rgba(255,255,255,0.1)
					font-size: 16px
					font-weight: 700
					color: #939499
					&.exist
						color: #fff
				.desc
					display: inline-block
					vertical-align: top
					margin: 13px 0 0 12px
					line-height: 24px
					font-size: 14px
					color: #939499
			.content-right
				flex: 0 0 105px
				width: 105px
				text-align: center
				line-height: 50px
				font-size: 14px
				font-weight: 700
				color: #969A9D
				background: #2B343B
				&.topay
					color: #fff
					background: #007E33
</style>
