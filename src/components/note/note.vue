<template>
	<li class="note">
		<ul class="note__options-list">
			<li class="options-list-option">
				<span 
					class="note__edit" 
					@click="$emit('show-edit', note)"
					title="edit"
				>&hellip;</span>
			</li>
			<li class="options-list-option">
				<span 
					class="note__remove" 
					@click="$emit('remove-note')"
					title="remove"
				>&times;</span>
			</li>
		</ul>
		<h3 class="note__title">{{note.title}}</h3>
		<p class="note__desc">{{note.desc}}</p>
		<p class="note__date">{{formatted}}</p>
	</li>
</template>

<script>
	import './note.scss'
	import formatting from '../../assets/libs/timeFormatting.js'

	export default {
		props: {
			note: {
				type: Object, 
				required: true
			}
		},
		data() {
			return {
				formatted: formatting(this.note.date)
			}
		},
		mounted() {
			setInterval(() => {
				this.formatted = formatting(this.note.date)
			}, 60000)
		}
	}
</script>