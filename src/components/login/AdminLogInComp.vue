<template>
  <div class="admin-login-comp">
    <h2>Admin</h2>
    <div class="admin-form-box">
      <h3>Email</h3>
      <input v-model="adminemail" type="email" />
      <h3>Password</h3>
      <input v-model="adminpassword" type="password" />

      <button v-on:click="adminLogIn" class="submit">LogIn</button>
    
      
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "AdminLogInComp",
  data() {
    return {
      adminemail: "",
      adminpassword: "",
    };
  },
  methods: {
    async adminLogIn() {
      let result = await axios.get(
        "http://localhost:3000/admin?email=" +
          this.adminemail +
          "&password=" +
          this.adminpassword
      );
      if (result.status == 200 && result.data.length > 0) {
        localStorage.setItem("admin-info", JSON.stringify(result));
        this.$router.push({ name: "HomeUser" });
      } else {
        console.log("password or email is wrong");
      }
    },
    signUpBox() {
      document.getElementById("loginbox").classList.toggle("scroll-down");
      document.getElementById("signupbox").classList.toggle("scroll-up");
    },
  },
  mounted() {
    let user = localStorage.getItem("admin-info");

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
.admin-login-comp {
  margin-left: 12%;
  width: 75%;
  height: 90%;
  color: $blueDarkCol;
  .admin-form-box {
    margin-top: 30%;
  }
}

  h2 {
    width: 40%;
    margin-left: 25%;
    height: 55px;
    font-style: italic;
    font-weight: 100;
    margin-top: 4%;
    font-size: 24px;
    margin-bottom: 7%;
    background: $greenYellCol;
    color: $blueDarkCol;
    border-left: 4px solid $blueDarkCol;

    border-bottom: 4px solid $blueDarkCol;

    font-family: "Bungee Inline", cursive;

    border-top-left-radius: 25%;
    border-bottom-right-radius: 25%;
  }

.admin-form-box {
  width: 100%;
  height: 80%;
  text-align: left;
  font-family: "Salsa", cursive;
  h3 {
    font-weight: normal;
    font-size: 17px;
  }
  input {
    width: 96%;
    height: 25px;
    margin-top: 4px;
    margin-bottom: 15px;
    margin-left: 0.3%;
    border-radius: 10%;
    padding-left: 2%;
    background: $greenYellCol;
    border: 1px;
    font-size: 16px;
  }
  h5 {
    width: 100%;
    margin-top: 25px;
    margin-bottom: 10px;
  }
  .submit {
    width: 25%;
    height: 35px;
    font-weight: 50;
    margin-left: 38%;
    border-radius: 15%;
    cursor: pointer;
    background: $blueDarkCol;
    color: $greenYellCol;
    font-family: "Luckiest Guy", cursive;
    letter-spacing: 1.2px;
    font-size: 15px;
    border: 1px;
    &:hover {
      border: 1px solid $greenYellCol;
      transition: 0.2s ease-in;
    }
  }
}


</style>
