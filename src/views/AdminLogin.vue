<template>
  <div class="login-admin-comp">
    <h2>Login</h2>
    <div class="form-box">
      <p>Email</p>
      <input v-model="email" type="email" />
      <p>Password</p>
      <input v-model="password" type="password" />

      <button v-on:click="logIn">Submit</button>
  
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "LogInAdminComp",
  data() {
    return {
      email: "",
      password: "",
    };
  },
  methods: {
    async logIn() {
      let result = await axios.get(
        "http://localhost:3000/admin?email" +
          this.email +
          "&password=" +
          this.password
      );
      if (result.status == 200 && result.data.length > 0) {
        localStorage.setItem("admin-info", JSON.stringify(result));
        this.$router.push({ name: "HomeAdmin" });
      }
      else{
          console.log("password or email is wrong");
      }
    },
 
  },
  mounted() {
    let admin = localStorage.getItem("admin-info");

    if (admin) {
      this.$router.push({ name: "HomeAdmin" });
    }
  },
};
</script>
<style lang="scss">
.login-admin-comp {
  margin-left: 25%;
  width: 50%;
  height: 100%;
  background: rgb(29, 31, 37);
}
#signup {
  cursor: pointer;
}
</style>
