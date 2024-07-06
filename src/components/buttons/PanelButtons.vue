<template>
    <div class="create-buttons">
        <div class="new-folder">
            <button @click="createFolder">
                <i class="bi bi-sticky-fill"></i>
                <p>New Folder</p>
            </button>
        </div>
        <div class="new-note">
            <button @click="createNote">
                <i class="bi bi-pen-fill"></i>
                <p>New Note</p>
            </button>
        </div>
    </div>
</template>
<script>
export default {
    data() {
        return {
            createFolderForm: false,
            createNoteForm: false
        }
    },
    methods: {
        createFolder() {
            this.$emit('toggle-folder-form');
            document.body.classList.add('form-show');
        },
        createNote() {
            this.$emit('toggle-note-form');
            document.body.classList.add('form-show');
        }
    }
}
</script>
