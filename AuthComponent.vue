<template>
    <div>
        <h2>Регистрация</h2>
        <form @submit.prevent="register">
            <div>
                <label for="registerName">Имя:</label>
                <input type="text" id="registerName" v-model="registerName">
            </div>
            <div>
                <label for="registerAge">Возраст:</label>
                <input type="text" id="registerAge" v-model="registerAge">
            </div>
            <button type="submit">Зарегистрироваться</button>
        </form>

        <h2>Авторизация</h2>
        <form @submit.prevent="login">
            <div>
                <label for="loginName">Имя:</label>
                <input type="text" id="loginName" v-model="loginName">
            </div>
            <button type="submit">Авторизоваться</button>
        </form>
    </div>  
</template>
  
<script>
import axios from 'axios';
  
export default {
name: 'AuthComponent',
data() {
    return{
        registerName: "",
        registerAge: '',
        loginName: ''
    }
},
methods: {
    async register() {
        const response = await axios.post('http://127.0.0.1:8000/users/', {
            name: this.registerName,
            age: Number(this.registerAge)
        });

        console.log('Register succes: ' + response.data);
    },
    async login() {
        try {
            const response = await axios.get(`http://127.0.0.1:8000/users/${this.loginName}`);
            if(response.data) {
                this.$emit('handleAuth', response.data);
            } else {
                alert ('Пользователь не найден');
            }
        } catch (error) {
            alert('Ошибка при авторизации');
        }
    }
}
}
  </script>

<style>
body {
  background-color: #fff8e1; /* Светло-серый фон */
  margin: 0;
  padding: 0;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
  
