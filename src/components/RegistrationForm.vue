<template>
  <div class="registration-form">
    <div>
      <label for="username">Username: </label>
      <input type="text" id="username" v-model="credentials.username" />
    </div>
    <div>
      <label for="password">Password: </label>
      <input type="password" id="password" v-model="credentials.password" />
    </div>
    <div>
      <label for="confirm-password">Confirm Password: </label>
      <input
        type="password"
        id="confirm-password"
        v-model="credentials.confirm_password"
      />
    </div>
    <div>
      <button @click="registration">submit</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "RegistrationForm",
  data: function () {
    return {
      credentials: {
        username: "",
        password: "",
        confirm_password: "",
      },
    };
  },
  methods: {
    registration: async function () {
      if (this.credentials.username.length < 5) {
        alert("username을 최소 5자 이상으로 입력해주세요.");
        return;
      }
      if (this.credentials.password.length < 5) {
        alert("password을 최소 5자 이상으로 입력해주세요.");
        return;
      }
      if (this.credentials.password != this.credentials.confirm_password) {
        alert("비밀번호가 일치하지 않습니다.");
        return;
      }
      const URL = "http://58.78.79.176:8000/accounts/signup/";
      const response = await fetch(URL, {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
          username: this.credentials.username,
          password: this.credentials.password,
        }),
      });

      // HTTP 상태 코드가 200과 299 사이일 경우 true
      if (response.ok) {
        const data = await response.json();
        this.$router.push({ name: "Login" });
        console.log(data.username);
      } else {
        alert("회원가입에 실패하였습니다.");
      }
    },
  },
};
</script>

<style></style>
