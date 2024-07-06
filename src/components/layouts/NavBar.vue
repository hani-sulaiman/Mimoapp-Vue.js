<template>
    <div class="nav">
        <div class="logo">
            <img :src="logoImg" alt="">
            <span>MIMO</span>
        </div>
        <h1>MY NOTES</h1>
        <div class="search">
            <i class="bi bi-search"></i>
            <input type="search" placeholder="Search" name="" id="">
        </div>
        <div class="user">
            <p>Hani Sulaiman</p>
        </div>

    </div>
</template>
<script>
export default{
    data(){
        return{
            logoImg:require('@/assets/img/logo.png'),
        }
    }
}
</script>
