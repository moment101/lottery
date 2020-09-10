<template>
	<div>
		<div class="input-group">
			<div class="input-group-prepend">
				<span class="input-group-text">貼上名單<br>一個一行</span>
			</div>
			<textarea class="form-control" aria-label="With textarea" v-model="items"></textarea>
		</div>
	</div>
</template>

<script>
	export default {
		props: {
			updateItems: Function
		},
		data() {
			return {
				items: [],
			}
		},
		watch: {
			items: function(newValue) {
				this.updateItems(newValue)
			}
		}
	}
</script>

<style>
	.input-group {
		height: 400px;
	}
</style>
