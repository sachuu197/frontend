<template>
  <div id="app">
    <nav class="navbar navbar-expand navbar-dark bg-dark">
      <a href class="navbar-brand" @click.prevent></a>
      <div class="navbar-nav mr-auto">
        <li class="nav-item">
          <router-link to="/home" class="nav-link">
            <font-awesome-icon icon="home" />Home
          </router-link>
        </li>
        <li v-if="showStudentBoard" class="nav-item">
          <router-link to="/student" class="nav-link">Student Board</router-link>
        </li>
        <li v-if="showGuideBoard" class="nav-item">
          <router-link to="/guide" class="nav-link">Guide Board</router-link>
        </li>
        <li v-if="showHodBoard" class="nav-item">
          <router-link to="/hod" class="nav-link">Hod Board</router-link>
        </li>
        <li v-if="showDirectorBoard" class="nav-item">
          <router-link to="/director" class="nav-link">Director Board</router-link>
        </li>
        <!-- <li class="nav-item">
          <router-link v-if="currentUser" to="/user" class="nav-link">User</router-link>
        </li> -->
      </div>

      <div v-if="!currentUser" class="navbar-nav ml-auto">
        <li class="nav-item">
          <router-link to="/register" class="nav-link">
            <font-awesome-icon icon="user-plus" />Sign Up
          </router-link>
        </li>
        <li class="nav-item">
          <router-link to="/login" class="nav-link">
            <font-awesome-icon icon="sign-in-alt" />Login
          </router-link>
        </li>
      </div>

      <div v-if="currentUser" class="navbar-nav ml-auto">
        <li class="nav-item">
          <router-link to="/profile" class="nav-link">
            <font-awesome-icon icon="user" />
            {{ currentUser.username }}
          </router-link>
        </li>
        <li class="nav-item">
          <a class="nav-link" href @click.prevent="logOut">
            <font-awesome-icon icon="sign-out-alt" />LogOut
          </a>
        </li>
      </div>
    </nav>

    <div class="container">
      <router-view />
    </div>
  </div>
</template>

<script>
export default {
  computed: {
    currentUser() {
      return this.$store.state.auth.user;
    },
    showStudentBoard() {
      if (this.currentUser && this.currentUser.roles) {
        return this.currentUser.roles.includes('ROLE_STUDENT');
      }

      return false;
    },
    showGuideBoard() {
      if (this.currentUser && this.currentUser.roles) {
        return this.currentUser.roles.includes('ROLE_GUIDE');
      }

      return false;
    },
      showHodBoard() {
      if (this.currentUser && this.currentUser.roles) {
        return this.currentUser.roles.includes('ROLE_HOD');
      }

      return false;
    },
      showDirectorBoard() {
      if (this.currentUser && this.currentUser.roles) {
        return this.currentUser.roles.includes('ROLE_DIRECTOR');
      }

      return false;
    }
  },
  methods: {
    logOut() {
      this.$store.dispatch('auth/logout');
      this.$router.push('/login');
    }
  }
};
</script>




<!-- <template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
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
-->