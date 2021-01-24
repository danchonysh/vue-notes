<template>
	<aside 
		:class="{
			'modal-bg': true,
			'show-modal': isVisible
		}"
		@click="closeEdit()">
		<form class="modal" @submit.prevent="edit()" @click.stop>
			<input 
				type="text" 
				v-model="editted.title" 
				class="modal__title" 
				placeholder="Title">
			<textarea 
				v-model="editted.desc" 
				class="modal__desc" 
				placeholder="Description">
			</textarea>
			<input class="modal__add" type="submit" value="Edit">
		</form>
	</aside>
</template>

<script>
import '../edit-modal/modal.scss'

export default {
	props: {
		isVisible: {
			Type: Boolean,
			required: true
		},
		editted: {
			Type: Object,
			required: true
		}
	}, 
	methods: {
		closeEdit() {
			this.$emit('close-edit')
		},
		edit() {
			if (this.editted.title.trim() !== '' && this.editted.desc.trim() !== '') {
				this.$emit('edit-note', this.editted)
				this.closeEdit()
			}
		}
	}
}
</script>