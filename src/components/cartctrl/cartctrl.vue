<template>
	<div class="cartctrl">
		<div class="decrease btn" v-show="food.count > 0" transition="move">
			<span class="btn-content" @click="decreaseCount">-</span>
		</div>
		<div class="count" v-show="food.count > 0">{{food.count}}</div>
		<div class="increase btn" @click="increaseCount">
			<span class="btn-content">+</span>
		</div>
	</div>
</template>

<script>
	import Vue from 'vue'

	export default {
		props : {
			food : {
				type : Object
			}
		},
		created () {

		},
		methods : {
			increaseCount : function () {
				if (!this.food.count) {
					Vue.set(this.food, 'count', 1)
				} else {
					this.food.count ++
				}
			},
			decreaseCount : function () {
				this.food.count --
			}
		}
	}
</script>

<style lang="stylus" rel="stylesheet/stylus">
	@import "../../common/stylus/mixin.styl"

	.cartctrl
		font-size: 0
		.btn
			display: inline-block
			width: 20px
			height: 20px
			border-radius: 10px
			background: #00A0DC
			text-align: center
			line-height: 20px
			.btn-content
				color: #fff
				font-weight: 700
				font-size: 16px
		.decrease
			font-size: 12px
			transition: all 0.4s linear
			&.move-transition
				opacity: 1
				transform: translate3D(0, 0, 0,)
			&.move-enter,&.move-leave
				opacity: 0
				transform: translate3D(24px, 0, 0)
		.count
			display: inline-block
			width: 20px
			text-align:center
			color: #969A9D
			font-size: 12px
		.increate
			font-size: 12px
</style>
