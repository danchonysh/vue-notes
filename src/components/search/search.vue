<template>
	<div class="search__wrapper">
		<input v-model="value" class="search" type="text" placeholder="Search">
	</div>
</template>

<script>
	import './search.scss'

	export default {
		props: {
			search: {
				type: String,
				required: true
			}
		},
		data () {
			return {
				value: this.search
			}
		},
		watch: {
			value(val) {
				this.$emit('search', val)
			}
		}
	}
</script>