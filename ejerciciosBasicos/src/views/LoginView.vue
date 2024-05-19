<template>
    <div class="Login">
        <h1>Login</h1>
        <form @submit.prevent="login">
        <input type="text" v-model="username" placeholder="Username" id="username"/>
        <input type="password" v-model="password" placeholder="Password" id="password" />
        <button type="submit">Login</button>
        </form>
    </div>
</template>
<script>
//Link del api 
const API_URL = 'https://apiusuarios-s9ff.onrender.com/api/user/login';
export default {
    data() {
        return {
            username: '',
            password: ''
        }
    },
    methods: {
        async login() {
            const response = await fetch(API_URL, {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify({
                    email: this.username,
                    password: this.password
                })
            });
            const data = await response.json();
            if (data.error) {
                alert(data.error);
            } else {
                localStorage.setItem('token', data.token);
                this.$router.push('/dashboard');
            }
        }
    }
}
</script>
<style>
.Login {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100vh;
}
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>