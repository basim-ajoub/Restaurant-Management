<template>
  <div class="login-comp">
    <h2>LogIn</h2>
    <div class="form-box">
      <h3>Email</h3>
      <input v-model="email" type="email" />
      <h3>Password</h3>
      <input v-model="password" type="password" />

      <button v-on:click="logIn" class="submit">LogIn</button>
      <h5>You Don't Have An Account !</h5>
      <h4 v-on:click="signUpBox" id="signup" class="signup-page">SignUp</h4>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "LogInComp",
  data() {
    return {
      email: "",
      password: "",
    };
  },
  methods: {
    async logIn() {
      let result = await axios.get(
        "http://localhost:3000/user?email=" +
          this.email +
          "&password=" +
          this.password
      );
      if (result.status == 200 && result.data.length > 0) {
        localStorage.setItem("user-info", JSON.stringify(result));
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
.login-comp {
  margin-left: 12%;
  width: 75%;
  height: 90%;
  color: $blueDarkCol;
  .form-box {
    margin-top: 30%;
  }
}//All Right Reserved B as im Aj ou b
.login-comp,
.signup-comp {
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
}
.form-box {
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
#signup {
  cursor: pointer;
  font-weight: bolder;
  background: $greenYellCol;
  width: 22%;
  height: 25px;
  text-align: center;
  border-radius: 20%;
}
.scroll-down {
  animation: scrolldown 1s forwards;
  animation-delay: 0.2s;
}
@keyframes scrolldown {
  0% {
    top: 0%;
  }
  100% {
    top: 100%;
  }
}
.scroll-up {
  animation: scrollup 1s forwards;
  animation-delay: 0.9s;
}
@keyframes scrollup {
  0% {
    top: 100%;
  }
  100% {
    top: 0%;
  }
}
</style>
