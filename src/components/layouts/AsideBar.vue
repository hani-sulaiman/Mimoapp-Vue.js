<template>
    <div :class="['aside', { 'open': isOpen, 'close': isClose }]">
        <div class="container-aside">
            <a href="" class="my-notes active">
                <i class="bi bi-journal"></i>
                <span>My Notes</span>
            </a>
            <button @click="signout" class="signout">
                <i class="bi bi-box-arrow-right"></i>
                <span>Sign Out</span>
            </button>
            <div class="slide-button" @click="slideHandle">
                <button>
                    <div class="container-button"><i class="bi bi-caret-right"></i></div>
                </button>
            </div>
        </div>

    </div>
</template>
<script>
import router from '@/router';
export default {
    data() {
        return {
            isOpen: false,
            isClose: true
        }
    },
    methods: {
        signout() {
            localStorage.removeItem('token');
            router.push('/login');
        }, slideHandle() {
            this.isClose = !this.isClose;
            this.isOpen = !this.isOpen;
        }
    }
}
</script>
<style scoped>
.signout {
    color: rgb(180, 180, 180);
    background: transparent;
    border: none;
    cursor: pointer;
    width: fit-content;
    font-size: 16px;
    padding: 0;
}
</style>
