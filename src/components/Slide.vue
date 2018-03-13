<template>
	<div class="slide">
		<img v-bind:src="slide.src" v-bind:alt="slide.alt" v-bind:title="slide.alt" />
	</div>
</template>

<script type="text/javascript">
	export default {
		data () {
			return {}
		},
		props: ['slide'],
	}
</script>

<style type="text/css" scoped="scoped">
.slide {
    display: inline-block;
}
.slide img {
    max-width: 100%;
}
</style>