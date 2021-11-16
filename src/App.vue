<template>
  <div id="app">
    <div id="nav">
      <div v-if="!isLogin">
        <router-link to="/">Home</router-link> |
        <router-link to="/login">Login</router-link> |
        <router-link to="/registration">Registration</router-link>
      </div>
      <div v-if="isLogin">
        <router-link to="/">Home</router-link> |
        <router-link @click.native="logout" to="#">Logout</router-link>
      </div>
    </div>
    <router-view />
  </div>
</template>

<script>
import { mapState } from "vuex";

export default {
  name: "App",
  data: function () {
    return {};
  },
  methods: {
    logout: function () {
      this.$store.state.isLogin = false;
      localStorage.removeItem("jwt");
      this.$router.push({ name: "Login" });
    },
  },
  created: function () {
    const token = localStorage.getItem("jwt");
    // 자동 로그인
    if (token) {
      this.$store.state.isLogin = true;
    }
  },
  computed: {
    ...mapState(["isLogin"]),
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
