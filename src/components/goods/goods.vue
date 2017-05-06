<template>
	<div class="goods">
		<div class="menu-wrap">
			<ul class="menu-list">
				<li v-for="item in goods" class="menu-item">
					<span class="text">
						<span v-show="item.type>-1" :class="classMap[item.type]" class="icon"></span>
						{{item.name}}
					</span>
				</li>
			</ul>
		</div>
		<div class="goods-wrap">
			<ul class="goods-list">
				<li v-for="item in goods" class="goods-item">
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
							</div>
						</li>
					</ul>
				</li>
			</ul>
		</div>
	</div>
</template>

<script>
	const ERR_OK = 0

	export default {
		props : {
			seller : {
				type : Object
			}
		},
		data () {
      return {
        goods: []
      }
    },
		created () {
      this.$axios.get('/api/goods').then(response => {
        var res = response.data
        if (res.errno === ERR_OK) {
          this.goods = res.data
        }
      })
      this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee']
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
					height: 54px
					line-height: 14px
					margin: 0 auto
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
			overflow: auto
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
									line-height: 10px;
									font-size: 10px
									color: rgb(147,153,159)
								.extra
									line-height: 10px
									color: 10px
									font-size: 10px
									.sell
										margin-right: 12px
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


</style>
