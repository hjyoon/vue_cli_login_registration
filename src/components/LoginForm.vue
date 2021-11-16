<template>
  <div class="login-form">
    <div>
      <label for="username">Username: </label>
      <input type="text" id="username" v-model="credentials.username" />
    </div>
    <div>
      <label for="password">Password: </label>
      <input type="password" id="password" v-model="credentials.password" />
    </div>
    <div>
      <button @click="login">submit</button>
    </div>
  </div>
</template>

<script>
//import { mapState } from "vuex";

export default {
  name: "LoginForm",
  data: function () {
    return {
      credentials: {
        username: "",
        password: "",
      },
    };
  },
  methods: {
    login: async function () {
      const URL = "http://58.78.79.176:8000/accounts/login/";
      const response = await fetch(URL, {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(this.credentials),
      });

      // HTTP 상태 코드가 200과 299 사이일 경우 true
      if (response.ok) {
        const data = await response.json();
        localStorage.setItem("jwt", data.token);
        this.$store.state.isLogin = true;
        this.$router.push({ name: "Home" });
      } else {
        alert("로그인에 실패하였습니다.");
      }
    },
  },
};
</script>

<style></style>
