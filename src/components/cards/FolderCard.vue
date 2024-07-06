<template>
    <div class="card">
        <div class="head">
            <i class="bi bi-sticky-fill"></i>
            <button @click="toggleOptionsFolder"> <i class="bi bi-three-dots"></i></button>
            <div class="options" v-if="isOpenOptions">
                <button @click="editFolder">Edit</button>
                <button @click="deleteFolder">Delete</button>
            </div>
        </div>
        <div class="body">
            <div class="title">{{ folder.title }}</div>
            <div class="details">{{ formatCreateFolderDate }}</div>
        </div>
    </div>
</template>
<script>
import axios from 'axios';
import draggable from 'vuedraggable';
export default {
    data() {
        return {
            isOpenOptions: false
        }
    },components:{
        draggable
    },
    props: {
        folder: Object
    },
    computed: {
        formatCreateFolderDate() {
            const date = new Date(this.folder.created_at);
            const year = date.getFullYear();
            const month = date.getMonth() + 1;
            const day = date.getDate();


            const formattedMonth = month < 10 ? `0${month}` : month;
            const formattedDay = day < 10 ? `0${day}` : day;

            return `${year}/${formattedMonth}/${formattedDay}`;
        }
    }, methods: {
        toggleOptionsFolder() {

            this.isOpenOptions = !this.isOpenOptions;
        },
        editFolder() {
            document.body.classList.add('form-show');
            this.$emit('trigger-edit-folder',this.folder);
            this.toggleOptionsFolder();
         },
        async deleteFolder() {
            try {
                axios.defaults.headers.common['Authorization'] = `Bearer ${localStorage.getItem('token')}`
                const baseURL = process.env.VUE_APP_API_URL;
                const folder = await axios.delete(`${baseURL}/folder/delete/${this.folder.id}`);
            } catch (error) {   }
            this.$emit('update-folders');
        }
    }
}
</script>
<style scoped>
.options {
    position: absolute;
    display: flex;
    flex-direction: column;
    align-items: start;
    background: #fff;
    padding: 5px;
    height: 60px;
    border-radius: 9px;
    justify-content: space-evenly;
    transition: 0.5s;
    right: -10px;
    top: 36px;
    animation-name: popup-options;
    animation-duration: 0.3s;
    animation-fill-mode: forwards;
}
@keyframes popup-options {
    from{
       transform:translateY(-20px) scale(0.7);
    }
    to{
        transform: translateY(0px) scale(1);
    }
}
.options button:nth-child(2) {

    color: red
}

.options button:nth-child(1) {
    border-bottom: 1px solid #00000024 !important;
    padding-bottom: 4px;
    color: rgb(0, 110, 255)
}
</style>