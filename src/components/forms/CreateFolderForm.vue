<template>
    <div :class="['form-popup', 'folder-form', { 'active': isOpenFolder }]">
        <div class="container-form">
            <form @submit.prevent="submitForm">
                <div class="head">
                    <input type="text" placeholder="Folder title goes here..." v-model="folder.title" class="title">
                    <button type="button" @click="closeForm" class="close-form"><i class="bi bi-x"></i></button>
                </div>
                <button type="submit"class="create">Create</button>
            </form>
        </div>
    </div>
</template>
<script>
import axios from 'axios';

export default {
    data(){
        return{
            folder:{
                title:'',
            }
        }
    },
    props: {
        isOpenFolder: Boolean,
    },
    methods: {
        closeForm() {
            this.$emit('close-form-folder');
            document.body.classList.remove('form-show');
        },
         async submitForm() {
            axios.defaults.headers.common['Authorization'] = `Bearer ${localStorage.getItem('token')}`
            const baseURL = process.env.VUE_APP_API_URL;
            const response = await axios.post(`${baseURL}/folder/create`,this.folder);
            this.$emit('update-folder-list');
            this.closeForm();
        },
    }
}
</script>
