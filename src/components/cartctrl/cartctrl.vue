<template>
	<div class="cartctrl">
		<div class="decrease btn" v-show="food.count > 0">
			<span class="btn-content">-</span>
		</div>
		<div class="count btn" v-show="food.count > 0">{{food.count}}</div>
		<div class="increase">
			<span class="btn-content">+</span>
		</div>
	</div>
</template>

<script>
	export default {
		props : {
			food : {
				type : Object
			}
		},
		created () {
			console.log(this.food)
		}
	}
</script>

<style lang="stylus" rel="stylesheet/stylus">
	@import "../../common/stylus/mixin.styl"

	.cartctrl
		font-size: 0
		.btn
			display: inline-block
			.btn-content
		.decrease
		.count
			display: inline-block
		.increate

</style>
