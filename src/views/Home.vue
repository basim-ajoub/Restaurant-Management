<template>
  <div class="home">
    <div class="left-fixed-box">
      <div class="title">
        <h1 class="restaurant-name">Ajjoub Restaurants</h1>
      </div>
      <div class="discription">
        <h4>Your World to Manage Your Restaurant</h4>
      </div>
    </div>
    <div class="scroller-div"></div>
    <div class="right-changed-box">
      <!--background box-->
      <div id="background-img-container" class="background-img-container"></div>
      <!--button login-->
      <button v-on:click="userLogIn" class="login-btn-box" id="login-btn">
        User LogIn
      </button>
      <!--button login as Admin-->
      <button
        v-on:click="adminLogIn"
        class="login-btn-box"
        id="login-admin-btn"
      >
        Admin LogIn
      </button>
      <!--login form box-->
      <div id="admin-login-form" class="admin-login-form login-form">
        <AdminLoginComp />
      </div>
      <div id="login-form" class="login-form">
        <div id="signupbox" class="signup log-box">
          <SigUpComp />
        </div>
        <div id="loginbox" class="login log-box">
          <LogInComp />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import SigUpComp from "../components/login/SignUpComp.vue";
import LogInComp from "../components/login/LogInComp.vue";
import AdminLoginComp from "../components/login/AdminLogInComp.vue";
export default {
  name: "Home",
  data() {
    return {
      username: "",
    };
  },
  components: {
    SigUpComp,
    LogInComp,
    AdminLoginComp,
  },
  methods: {
    userLogIn() {
      document
        .getElementById("background-img-container")
        .classList.toggle("fade");
      var topValue = document.getElementById("login-form").style.top;
      if (topValue == "-600px") {
        document.getElementById("login-form").classList.toggle("show");
        document.getElementById("login-form").style.top = "80px";
        document.getElementById("login-form").style.right = "15%";
      } else {
        document.getElementById("login-form").classList.toggle("show");
      }

      document.getElementById("login-btn").style.display = "none";
      document.getElementById("login-admin-btn").style.display = "block";
      //   var rightAdminvalue = document.getElementById("admin-login-form").style.right;

      document.getElementById("admin-login-form").style.display = "none";
    },
    adminLogIn() {
      document.getElementById("login-btn").style.display = "block";
      document.getElementById("login-admin-btn").style.display = "none";
      document.getElementById("background-img-container").style.display =
        "none";
      document.getElementById("login-form").style.top = "-600px";
      document.getElementById("admin-login-form").style.display = "block";
    },
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
.home {
  width: 100%;
  height: 100%;
  background-image: linear-gradient(30deg, $redCol, $whitCol);
  overflow: hidden;

  .left-fixed-box {
    width: 50%;
    height: 100%;
    position: relative;
    transform: skewX(-18deg);
    float: left;
    background: $blueDarkCol;
    margin-left: -12%;
    z-index: 3;
    // border-right: 4px solid $blueCol;

    .title {
      width: 95%;
      height: 130px;
      margin-left: 9%;
      margin-top: 110px;
      font-family: "Puppies Play", cursive;

      letter-spacing: 4px;
      font-size: 25px;
      .restaurant-name {
        text-shadow: 0px 2px 5px $redCol;
        font-size: 35px;
        font-family: "Luckiest Guy", cursive;
        font-family: "Skranji", cursive;

        font-weight: normal;
        font-family: "Bungee Inline", cursive;
        color: $greenYellCol;
      }
    }
    .discription {
      margin-top: 50px;
      width: 70%;
      height: 100px;
      margin-left: 24%;
      color: $greenYellCol;
    }
  }
  .scroller-div {
    width: 5%;
    height: 10%;
    position: absolute;
    left: 42%;
    background: $greenYellCol;
    z-index: 20;
    top: 0;
    display: none;
    &:hover {
    }
  }
  .right-changed-box {
    width: 70%;
    height: 100%;
    position: relative;
    // background: $redCol;
    background-image: linear-gradient(30deg, $redCol, $whitCol);
    z-index: 2;
    left: 30%;

    .background-img-container {
      width: 100%;
      height: 100%;
      display: block;
      position: absolute;
      top: 0;
      background-image: url("../../public/header-background-1.jpg");
      background-size: cover;
      transition: ease-in 0.4s;
    }
    // start background  fade
    .fade {
      animation: fade 1s forwards;
      animation-delay: 0.2s;
    }

    @keyframes fade {
      0% {
        left: 0%;
      }

      100% {
        left: -100%;
      }
    }
    //Start admin LogIn form
    #login-admin-btn {
      display: none;
    }
    //End admin LogIn form
    // end background  fade
    .login-btn-box {
      width: 10%;
      height: 35px;
      background: $blueDarkCol;
      cursor: pointer;
      position: absolute;
      right: 4%;
      top: 30px;
      text-align: center;
      color: $greenYellCol;
      border-radius: 10%;

      font-weight: bold;
    }
    .login-form {
      width: 50%;
      height: 550px;

      position: absolute;
      top: 80px;
      right: -100%;
      overflow: hidden;
      transition: ease-in-out 0.4s;
      .log-box {
        width: 98%;
        height: 98%;
        z-index: 2;
        position: absolute;

        color: $blueDarkCol;
        border-radius: 1%;
        border-top-left-radius: 15%;
        border-bottom-right-radius: 15%;
        padding-top: 10px;
      }
      #signupbox {
        top: 100%;
      }
      #loginbox {
        top: 0%;
      }
    }
    // start login form  show
    .show {
      animation: show 2s forwards;
      animation-delay: 0.1s;
    }
    @keyframes show {
      0% {
        right: -100%;
      }
      100% {
        right: 16%;
      }
    }
    // end login form  show
    //admin login form
    .admin-login-form {
      right: 120%;
      display: none;
      animation: adminshow 2s forwards;
      animation-delay: 0.1s;
    }
    @keyframes adminshow {
      0% {
        right: 120%;
      }
      100% {
        right: 18%;
      }
    }
  }
}
</style>
