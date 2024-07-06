<template>
  <div class="container">
    <NavBar />
    <div class="main">
      <AsideBar />
      <Home ref="homeContent" @open-edit-folder="openEditfolder" @button-panel-note-clicked="toggleNoteForm"
        @button-panel-folder-clicked="toggleFolderForm" />
    </div>
  </div>
  <CreateNoteForm @update-note-list="refreshNotes" :isOpenNote="isNoteFormOpen" @close-form-note="closeNoteForm" />
  <CreateFolderForm @update-folder-list="refreshFolders" :isOpenFolder="isFolderFormOpen"
    @close-form-folder="closeFolderForm" />
  <EditFolderFrom v-if="this.isOpenEditFormFolder" :folderData="editFolder" />
  <FloatingButtons @toggle-folder-form="toggleFolderForm" @toggle-note-form="toggleNoteForm" />

</template>
<script>
import Home from "@/components/home/HomeContent.vue";
import AsideBar from '@/components/layouts/AsideBar.vue'
import NavBar from '@/components/layouts/NavBar.vue'
import FloatingButtons from '@/components/buttons/FloatingButtons.vue'
import CreateFolderForm from '@/components/forms/CreateFolderForm.vue'
import CreateNoteForm from '@/components/forms/CreateNoteForm.vue'
import EditFolderFrom from "@/components/forms/EditFolderFrom.vue";
export default {
  data() {
    return {
      isFolderFormOpen: false,
      isNoteFormOpen: false,
      isOpenEditFormFolder: false,
      editFolder: null
    }
  },
  components: {
    Home, AsideBar, NavBar, FloatingButtons, CreateFolderForm, CreateNoteForm, EditFolderFrom
  }, methods: {
    toggleFolderForm() {
      this.isFolderFormOpen = !this.isFolderFormOpen;
    },
    closeFolderForm() {
      this.isFolderFormOpen = false;
      this.isOpenEditFormFolder = false;
      
    },
    toggleNoteForm() {
      this.isNoteFormOpen = !this.isNoteFormOpen;
    },
    closeNoteForm() {
      this.isNoteFormOpen = false;
    },
    refreshFolders() {
      this.$refs.homeContent.updateFolders();
    }, refreshNotes() {
      this.$refs.homeContent.updateNotes();
    }, openEditfolder(folder) {
      this.editFolder = folder;
      this.isOpenEditFormFolder = true;
    }
  }
}
</script>