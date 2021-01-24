<template>
	<ul class="notes">
		<Note 
			v-for="(note, index) in notes" :key="note.desc" :note="note" 
			@show-edit="$emit('show-edit', {index, ...$event})"
			@remove-note="$emit('remove-note', index)"/>
	</ul>
</template>

<script>
	const toLocal = notes => localStorage.setItem('notes', JSON.stringify(notes))

	import Note from '../note/note'
	import './notes.scss'

	export default {
		components: {
			Note
		},
		props: {
			notes: {
				type: Array,
				required: true
			}
		}
	}
</script>