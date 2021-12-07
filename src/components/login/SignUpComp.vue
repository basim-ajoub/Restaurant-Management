<template>
  <div class="signup-comp">
    <h2>SignUp</h2>
    <div class="form-box">
      <h3>First Name</h3>
      <input v-model="firstname" type="text" />
      <h3>Last Name</h3>
      <input v-model="lastname" type="text" />
      <h3>Email</h3>
      <input v-model="email" type="email" />
      <h3>Password</h3>
      <input v-model="password" type="password" />
      <h3>Re-Passwoord</h3>
      <input type="password" />
      <button v-on:click="signUp" class="submit">SignUp</button>
      <h5>Do You Have An Account !</h5>
      <h4 v-on:click="logInBox" id="login" class="login-page">LogIn</h4>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "SignUpComp",
  data() {
    return {
      firstname: "",
      lastname: "",
      name: "",
      email: "",
      password: "",
    };
  },
  methods: {
    async signUp() {
      let result = await axios.post("http://localhost:3000/user", {
        name: this.firstname + this.lastname,
        email: this.email,
        password: this.password,
        id: this.id,
      });
      if (result.status == 201) {
        localStorage.setItem("user-info", JSON.stringify(result));
        this.$router.push({ name: "HomeUser" });
      }
    },
    logInBox() {
      document.getElementById("signupbox").classList.remove("scroll-up");
      document.getElementById("loginbox").classList.remove("scroll-down");
    },
  },
  mounted() {
    let user = localStorage.getItem("user-info");

    if (user) {
      this.$router.push({ name: "HomeUser" });
    }
  },
};
</script>
<style lang="scss">
$blueCol: #024566;
$yellowCol: #f5d9a6;
$redCol: #b37a79;
$braunCol: #512415;
$blueDarkCol: #111324;
$yellowCol: #f5d9a6;
$skyCol: #51cfdb;
$whitCol: #ffff;
$purpleCol: #7856ff;
$greenYellCol: #cdd400;
.signup-comp {
  margin-left: 12%;
  width: 75%;
  height: 90%;

  #login {
    cursor: pointer;
    background: $greenYellCol;
    width: 22%;
    font-weight: bolder;
    height: 25px;
    text-align: center;
    border-radius: 20%;
  }
}
</style>
