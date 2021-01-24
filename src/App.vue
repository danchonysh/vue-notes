<template>
    <div class="wrapper">
		<h1>Notes</h1>
		<Message v-if="message"/>
		<NewNote 
			:note="note" 
			@addNote="addNote"/>
		<Search 
			:search="search" 
			@search="search = $event"/>
		<Notes 
			:notes="filteredNotes ? filteredNotes : sorted"
			@show-edit="showEdit($event)"
			@remove-note="removeNote($event)"/>
		<EditModal 
			:editted="editted"
			:isVisible="isVisible"
			@close-edit="isVisible = false"
			@edit-note="edit($event)"/>
    </div>
</template>

<script>
const toLocal = notes => localStorage.setItem('notes', JSON.stringify(notes))

import Message from './components/message/message'
import NewNote from './components/new-note/new-note'
import Notes from './components/notes/notes'
import Search from './components/search/search'
import EditModal from './components/edit-modal/modal'

export default {
	components: {
			Message,
			NewNote,
			Notes,
			Search,
			EditModal
		},
	data() {
		return {
			message: false,
			search: '',
			note: {
				title: '',
				desc: ''
			},
			isVisible: false,
			editted: {},
			notes: JSON.parse(localStorage.getItem('notes')) ? JSON.parse(localStorage.getItem('notes')) : []
		}
	},
	methods: {
		addNote() {
			let {title, desc} = this.note
			if (title.trim() === '' || desc.trim() === '') {
				this.message = true
			} else {
				this.message = false
				this.notes.push({
					title,
					desc,
					date: new Date(Date.now()).toLocaleString()
				})
				this.note.title = ''
				this.note.desc = ''
			}
			toLocal(this.notes)
		},
		removeNote(index) {
			this.notes.splice(index, 1)
			toLocal(this.notes)
		},
		showEdit(data) {
			this.isVisible = true
			this.editted = data
		},
		edit(data) {
			this.notes[this.editted.index].title = data.title
			this.notes[this.editted.index].desc = data.desc
			this.notes[this.editted.index].date = new Date(Date.now()).toLocaleString()
			toLocal(this.notes)
		}
	},
	computed: {
		sorted() {
			return this.notes.sort((a,b) => 
				Date.parse(new Date(b.date)) - 
				Date.parse(new Date(a.date))
			)
		},
		filteredNotes() {
			const isConsist = (substring, array) => 
				array.filter(el =>
					el.toLowerCase().includes(substring.trim().toLowerCase())
				).length
			const notes = this.notes, search = this.search
			return !search ? false : notes.filter(el =>
					isConsist(search, [el.title, el.desc, el.date])
			)
		}
	}	
}	
</script>
