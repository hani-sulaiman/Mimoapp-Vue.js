<template>
    <div :class="['form-popup', 'note-form', { 'active': isOpenNote }]">
        <div class="container-form">
            <form @submit.prevent="submitForm">
                <div class="head">
                    <input type="text" placeholder="Title goes here..." v-model="noteData.title" class="title">
                    <button type="button" @click="closeForm" class="close-form"><i class="bi bi-x"></i></button>
                </div>
                <div class="content">
                    <textarea name="" id="" v-model="noteData.content" placeholder="Your note goes here..."></textarea>
                </div>
                <button class="create">Create</button>
            </form>
        </div>
    </div>
</template>
<script>
import axios from 'axios';

export default {
    data(){
        return{
            noteData:{
                title:'',
                content:''
            }
        }
    },
    props: {
        isOpenNote: Boolean,
    },
    methods: {
        closeForm() {
            this.$emit('close-form-note');
            document.body.classList.remove('form-show');
        },
        async submitForm() {
            axios.defaults.headers.common['Authorization'] = `Bearer ${localStorage.getItem('token')}`
            const baseURL = process.env.VUE_APP_API_URL;
            const response = await axios.post(`${baseURL}/note/create`,this.noteData);
            this.$emit('update-note-list');
            this.closeForm();
        },
    }
}
</script>
