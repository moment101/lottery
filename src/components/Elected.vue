<template>
	<div>
		<div class="input-group">
			<div class="input-group-prepend">
				<span class="input-group-text">中獎者</span>
			</div>
			<textarea class="form-control" aria-label="With textarea" :value="selectedItems_str" readonly></textarea>
		</div>
	</div>
</template>

<script>
	export default {
		props: {
			selectedItems_str: Object
		},
		data() {
			
		},
	}
</script>

<style>
	.input-group {
		height: 400px;
	}
</style>
