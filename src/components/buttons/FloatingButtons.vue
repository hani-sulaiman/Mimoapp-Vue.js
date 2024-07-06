<template>
    <div class="floating-buttons">
        <button class="floating-button">
            <div :class="['container-floating',{ 'open': isOpen, 'close': isClose }]" @click="floatingButtonHandle">
                <i class="bi bi-plus"></i>
            </div>
        </button>
        <div :class="['nested-floating-buttons', { 'open': isOpen, 'close': isClose }]">
            <div class="container-buttons">
                <button class="add-folder" @click="createFolder"><i class="bi bi-sticky-fill"></i></button>
                <button class="add-note" @click="createNote"> <i class="bi bi-pen-fill"></i></button>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    data() {
        return {
            isOpen: false,
            isClose: true,
            createFolderForm: false,
            createNoteForm: false
        }
    },
    methods: {
        floatingButtonHandle() {
            this.isClose = !this.isClose;
            this.isOpen = !this.isOpen;
        }
        ,
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
