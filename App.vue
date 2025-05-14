<template>
  <div id="app">
    <auth-component v-if="!isAuth" @handleAuth="handleAuth" />
    <div v-else>
      <p>Вы авторизованный красавчик</p>
      <p>Имя: {{ user.name }}</p>
      <p>Возраст: {{ user.age }}</p>  
    </div>
  </div>
</template>

<script>
import AuthComponent from './components/AuthComponent.vue'

export default {
  name: 'App',
  components: {
    AuthComponent
  }, 
  data() {
    return{
      isAuth: false,
      user: null,
    }
  },
  methods: {
    handleAuth(userData) {
      this.isAuth = true;
      this.user = userData; 
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
