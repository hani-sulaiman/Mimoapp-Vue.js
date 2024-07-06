<template>
    <div class="notes">
        <div class="container-notes">
            <div class="section folders">
                <h2>Recent Folders</h2>
                <div class="buttons">
                    <a href="" class="active">Todays</a>
                    <a href="">This Week</a>
                    <a href="">This Month</a>
                </div>
                <div v-if="loadedFolders" class="cards">
                    <FolderCard v-for="folder in folders" :folder="folder" @trigger-edit-folder="triggerOpenFolder" @update-folders="updateFolders" />
                </div>
                <content-loader v-else class="content-loader">
                    <rect x="0" y="0" rx="5" ry="5" width="30%" height="100%" />
                    <rect x="35%" y="0" rx="5" ry="5" width="30%" height="100%" />
                    <rect x="70%" y="0" rx="5" ry="5" width="30%" height="100%" />
                </content-loader>
            </div>
            <div class="section my-notes">
                <h2>My Notes</h2>
                <div class="buttons">
                    <a href="" class="active">Todays</a>
                    <a href="">This Week</a>
                    <a href="">This Month</a>
                </div>
                <div v-if="loadedNotes" class="cards">
                    <NoteCard v-for="note in notes" :note="note" />
                </div>
                <content-loader v-else class="content-loader">
                    <rect x="0" y="0" rx="5" ry="5" width="30%" height="100%" />
                    <rect x="35%" y="0" rx="5" ry="5" width="30%" height="100%" />
                    <rect x="70%" y="0" rx="5" ry="5" width="30%" height="100%" />
                </content-loader>
            </div>
        </div>
        <PanelButtons @toggle-folder-form="buttonPanelFolderClicked" @toggle-note-form="buttonPanelNoteClicked" />
    </div>
</template>
<script>
import FolderCard from '@/components/cards/FolderCard.vue';
import NoteCard from '@/components/cards/NoteCard.vue';
import PanelButtons from '@/components/buttons/PanelButtons.vue';
import axios from 'axios';
import { ContentLoader } from 'vue-content-loader'
export default {
    props: {
        addFolders: Function
    },
    data() {
        return {
            loadedFolders: false,
            loadedNotes: false,
            notes: [],
            folders: []
        }
    },
    components: {
        PanelButtons, FolderCard, NoteCard, ContentLoader
    }
    , async mounted() {
        axios.defaults.headers.common['Authorization'] = `Bearer ${localStorage.getItem('token')}`
        const baseURL = process.env.VUE_APP_API_URL;
        const Notes = await axios.get(`${baseURL}/note/all`);
        this.notes = Notes.data.notes;
        const Folders = await axios.get(`${baseURL}/folder/all`);
        this.folders = Folders.data.folders;
        this.loadedNotes =true;
        this.loadedFolders=true;
    }
    , methods: {
        async updateFolders() {
            this.loadedFolders=false;
            axios.defaults.headers.common['Authorization'] = `Bearer ${localStorage.getItem('token')}`
            const baseURL = process.env.VUE_APP_API_URL;
            const Folders = await axios.get(`${baseURL}/folder/all`);
            this.folders = Folders.data.folders;
            this.loadedFolders=true;
        },
        async updateNotes() {
            this.loadedNotes =false;
            axios.defaults.headers.common['Authorization'] = `Bearer ${localStorage.getItem('token')}`
            const baseURL = process.env.VUE_APP_API_URL;
            const Notes = await axios.get(`${baseURL}/note/all`);
            this.notes = Notes.data.notes;
            this.loadedNotes =true;
        }
         ,buttonPanelNoteClicked(){
            this.$emit('button-panel-note-clicked');
        }
         ,buttonPanelFolderClicked(){
            this.$emit('button-panel-folder-clicked');
        },triggerOpenFolder(folder){
            this.$emit('open-edit-folder',folder);
        }
    }

}
</script>
<style scoped>
.content-loader {
    margin-top: 30px;
    transition: 0.5s;
}
</style>