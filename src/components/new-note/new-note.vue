<template>
	<form class="new-note" @submit="addNote">
		<h2>Add note: </h2>
		<input type="text" v-model="note.title" class="new-note__title" placeholder="Title">
		<textarea v-model="note.desc" class="new-note__desc" placeholder="Description"></textarea>
		<input class="new-note__add" type="submit" value="Add">
	</form>
</template>

<script>
	import './new-note.scss'

	export default {
		props: {
			note: {
				type: Object,
				required: true
			}
		},
		methods: {
			addNote (e) {
				e.preventDefault()
				this.$emit('addNote', this.note)
			}
		}
	}
</script>