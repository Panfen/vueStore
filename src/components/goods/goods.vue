<template>
	<div class="goods">
		<div class="menu-wrap" ref="menuwrapper">
			<ul class="menu-list">
				<li v-for="(item, index) in goods" class="menu-item" :class="{'current' : currentIndex === index}" v-on:click="selectMenu(index)">
					<span class="text">
						<span v-show="item.type>-1" :class="classMap[item.type]" class="icon"></span>
						{{item.name}}
					</span>
				</li>
			</ul>
		</div>
		<div class="goods-wrap" ref="goodswrapper">
			<ul class="goods-list">
				<li v-for="item in goods" class="goods-item goods-item-hook">
					<h1 class="title">{{item.name}}</h1>
					<ul class="foods-list">
						<li v-for="food in item.foods" class="foods-item">
							<img :src="food.icon" class="icon">
							<div class="content">
								<h2 class="name">{{food.name}}</h2>
								<p class="description">{{food.description}}</p>
								<div class="extra">
									<span class="sell">月售{{food.sellCount}}份</span>
									<span class="rating">好评率{{food.rating}}</span>
								</div>
								<div class="price">
									<span class="now">¥{{food.price}}</span>
									<span v-show="food.oldPrice" class="old">¥{{food.oldPrice}}</span>
								</div>
								<div class="cartwrap">
									<cartctrl :food="food"></cartctrl>
								</div>
							</div>
						</li>
					</ul>
				</li>
			</ul>
		</div>
		<shopcart :selectedFoods="selectedFoods" :delivery-price="seller.deliveryPrice" :min-price="seller.minPrice"></shopcart>
	</div>
</template>

<script>
	import BScroll from 'better-scroll'
	import shopcart from '@/components/shopcart/shopcart.vue'
	import cartctrl from '@/components/cartctrl/cartctrl.vue'

	const ERR_OK = 0

	export default {
		props : {
			seller : {
				type : Object
			}
		},
		data () {
      return {
        goods: [],
        heightList : [],
        scrollY : 0
      }
    },
    computed : {
			currentIndex : function () {
				for (var i = 0; i < this.heightList.length; i++) {
					var height1 = this.heightList[i]
					var height2 = this.heightList[i + 1]
					if (!height2 || (this.scrollY >= height1 && this.scrollY < height2)) {
						return i
					}
				}
				return 0
			},
			selectedFoods : function () {
				var foods = []
				this.goods.forEach((good) => {
					good.foods.forEach((food) => {
						if (food.count > 0) {
							foods.puah(food)
						}
					})
				})
				return foods
			}
    },
		created () {
      this.$axios.get('/api/goods').then(response => {
        var res = response.data
        if (res.errno === ERR_OK) {
          this.goods = res.data
          this.$nextTick(() => {
						this._initScroll()
						this._calculateHeight()
          })
        }
      })
      this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee']
    },
    methods : {
			_initScroll : function () {
				this.menuScroll = new BScroll(this.$refs.menuwrapper, {
					click : true
				})
				this.goodsScroll = new BScroll(this.$refs.goodswrapper, {
					click : true,
					probeType : 3
				})
				this.goodsScroll.on('scroll', (pos) => {
					this.scrollY = Math.abs(Math.round(pos.y))
				})
			},
			_calculateHeight : function () {
				var foodList = this.$refs.goodswrapper.getElementsByClassName('goods-item-hook')
				var height = 0
				this.heightList.push(height)
				for (var i = 0; i < foodList.length; i++) {
					var item = foodList[i]
					height += item.clientHeight
					this.heightList.push(height)
				}
			},
			selectMenu : function (index) {
				var foodList = this.$refs.goodswrapper.getElementsByClassName('goods-item-hook')
				var el = foodList[index]
				this.goodsScroll.scrollToElement(el, 300)
			}
    },
    components : {
			shopcart,
			cartctrl
    }
	}
</script>

<style lang="stylus" rel="stylesheet/stylus">
	@import "../../common/stylus/mixin.styl"

	.goods
		display: flex
		position: absolute
		top: 186px
		bottom: 46px
		width: 100%
		overflow: hidden
		.menu-wrap
			flex: 0 0 80px
			width: 80px
			background: #f3f5f7
			.menu-list
				.menu-item
					display: table
					width: 56px
					padding: 0 12px
					height: 54px
					line-height: 14px
					margin: 0 auto
					&.current
						position: relative
						z-index: 10
						background: #fff
						font-weight: 700
						.text
							border-1px(rgba(7, 17, 27, 0))
					.icon
						display: inline-block
						vertical-align:	top
						width: 12px
						height: 12px
						margin-right: 2px
						background-size: 12px 12px
						background-repeat: no-repeat
						&.decrease
							bg-image("./img/decrease_3")
						&.discount
							bg-image("./img/discount_3")
						&.guarantee
							bg-image("./img/guarantee_3")
						&.invoice
							bg-image("./img/invoice_3")
						&.special
							bg-image("./img/special_3")
					.text
						display: table-cell
						width: 56px
						vertical-align: middle
						border-1px(rgba(7, 17, 27, 0.1))
						font-size: 12px	
		.goods-wrap
			flex: 1
			.goods-list
				.goods-item
					.title
						padding-left: 14px
						height: 26px
						line-height: 26px
						border-left: 2px solid #d9dde1
						font-size: 12px
						color: rgb(147,153,159)
						background: #f3f5f7
					.foods-list
						.foods-item
							display: flex
							margin: 18px
							padding-bottom: 18px
							border-1px(rgba(7, 17, 27, 0.1))
							&:last-child
								border-none()
								padding-bottom: 0
							.icon
								flex: 0 0 56px
								width: 56px
								height: 56px
								margin-right: 10px
							.content
								flex: 1
								.name
									margin: 2px 0 8px 0
									height: 14px
									line-height: 14px
									font-size: 14px
									color: rgb(7,17,27)
								.description
									margin-bottom: 8px
									line-height: 12px;
									font-size: 10px
									color: rgb(147,153,159)
								.extra
									line-height: 10px
									color: 10px
									font-size: 10px
									.sell
										margin-right: 8px
								.price
									font-weight: 700
									line-height: 24px
									.now
										margin-right: 8px
										font-size: 14px
										color: rgb(240,20,20)
									.old
										text-decoration: line-through
										font-size: 10px;
										color: rgb(147,153,159)
								.cartwrap
									position: absolute
									bottom: 18px
									right: 0px
									text-align: right

</style>
