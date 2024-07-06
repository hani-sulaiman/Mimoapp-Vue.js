<template>
    <div class="container">
        <form class="login-form" @submit.prevent="signup">
            <h2>Signup</h2>
            <div class="input-group">
                <label for="fullname">Fullname:</label>
                <input type="text" id="fullname" v-model="signupData.name" placeholder="Enter your Fullname" required>
            </div>
            <div class="input-group">
                <label for="email">Email:</label>
                <input type="email" id="email" v-model="signupData.email" placeholder="Enter your email" required>
            </div>
            <div class="input-group">
                <label for="password">Password:</label>
                <input type="password" id="password" v-model="signupData.password" placeholder="Enter your password"
                    required>
            </div>
            <div class="input-group">
                <p style="color: red;">{{ errorMessage }}</p>
            </div>
            <LoadingButton/>
        </form>
    </div>
</template>
<script>
import axios from 'axios';
import router from '@/router'; 
import LoadingButton from '@/components/buttons/LoadingButton.vue';
export default {
    components:{
        LoadingButton
    }
    ,
    data() {
        return {
            loading: false,
            errorMessage: '',
            signupData: {
                name:'',
                email: '',
                password: ''
            }
        }
    }, methods: {
        async signup() {

            this.loading = true;
            const baseURL = process.env.VUE_APP_API_URL;
            const response = await axios.post(`${baseURL}/signup`, this.signupData, {
                headers: {
                    'Accept': 'application/json'
                }
            });
            this.loading = false;
            localStorage.setItem('token', response.data.token);
            router.push('/');
        }
    }
}
</script>
<style scoped>
body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
    background-color: #f2f2f2;
}

.container {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
}

.login-form {
    background-color: #ffffff;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    width: 80%;
    max-width: 400px;
}

h2 {
    margin-bottom: 20px;
    text-align: center;
}

.input-group {
    margin-bottom: 15px;
}

.input-group label {
    display: block;
    margin-bottom: 5px;
}

.input-group input {
    width: 95%;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
}

button {
    width: 100%;
    padding: 10px;
    background-color: #007bff;
    color: #ffffff;
    border: none;
    border-radius: 5px;
    cursor: pointer;
}

button:hover {
    background-color: #0056b3;
}

@media screen and (max-width: 768px) {
    .login-form {
        width: 90%;
    }
}
</style>