<template>
  <div id="app" class="home-user">
    <div id="welcome-text" class="welcome-text">
      <h1>
        Welcome <span class="user-font-change"> {{ username }}</span> to Your
        Home Page
      </h1>
    </div>
    <div
      id="nav-hover"
      @mouseover="navShow"
      @mouseleave="navHidden"
      class="nav"
    >
      <div class="user-name-box">
        <h3 id="nav-user-name">{{ username }}</h3>
      </div>

      <ul class="nav-list">
        <!--food selection show only in admin panel-->
        <li
          id="analysis-selection"
          class="analysis-selection"
          @mouseover="navShow"
          @mouseleave="navHidden"
          v-on:click="analysisBtn"
        >
          <router-link id="analysis-title" class="nav-title" to="/user/home/"
            >Analysis</router-link
          >
          <a id="analysis-icon" class="list-icon" href="#"
            ><i class="fas fa-chart-bar"></i>
          </a>
          <fontawesome-icon
            class="delivery-icon"
            :icon="['fas', 'shipping-fast']"
          />
        </li>
        <!--information selection show only in user panel-->
        <li
          @mouseover="navShow"
          @mouseleave="navHidden"
          v-on:click="infoBtn"
          id="information-btn"
        >
          <router-link
            id="informations-title"
            @click="this.showOrders"
            class="nav-title"
            to="/user/home/"
            >Informations</router-link
          ><a class="list-icon" id="informations-icon" href="#"
            ><i class="fas fa-chart-bar"></i>
          </a>
          <fontawesome-icon
            class="delivery-icon"
            :icon="['fas', 'shipping-fast']"
          />
        </li>
        <li @mouseover="navShow" @mouseleave="navHidden" v-on:click="billBtn">
          <router-link id="bills-title" class="nav-title" to="/user/home/"
            >Bills</router-link
          >
          <a id="bills-icon" class="list-icon" href="#"
            ><i class="fas fa-money-check-alt"></i>
          </a>
          <fontawesome-icon
            class="delivery-icon"
            :icon="['fas', 'shipping-fast']"
          />
        </li>
        <!--food selection show only in admin panel-->
        <li
          id="food-selection"
          class="food-selection"
          @mouseover="navShow"
          @mouseleave="navHidden"
          v-on:click="foodBtn"
        >
          <router-link id="foods-title" class="nav-title" to="/user/home/"
            >Foods</router-link
          >
          <a id="foods-icon" class="list-icon" href="#"
            ><i class="fas fa-utensils"></i>
          </a>
          <fontawesome-icon
            class="delivery-icon"
            :icon="['fas', 'shipping-fast']"
          />
        </li>
        <li @mouseover="navShow" @mouseleave="navHidden" v-on:click="orderBtn">
          <router-link id="orders-title" class="nav-title" to="/user/home/"
            >Order</router-link
          ><a id="orders-icon" class="list-icon" href="#"
            ><i class="fa fa-edit"></i
          ></a>
          <fontawesome-icon
            class="delivery-icon"
            :icon="['fas', 'shipping-fast']"
          />
        </li>
      </ul>
      <button
        @mouseover="navShow"
        @mouseleave="navHidden"
        @click="logOut"
        id="logout-btn"
        class="logout-btn"
      >
        SignOut
      </button>
      <button
        @mouseover="navShow"
        @mouseleave="navHidden"
        @click="logOut"
        id="logout-btn-change"
        class="logout-btn-change logout-btn"
      >

        <i class="fas fa-sign-out-alt"></i>
      </button>
    <p id="right-title">All Right Reserved Basim Ajoub</p>
    </div>

    <div id="container" class="container">
      <div id="info-box" class="show-component information-box">
        <UserInformationComp :username="this.username" />
      </div>
      <div id="bill-box" class="show-component bill-box">
        <UserBillComp />
      </div>
      <div id="order-box" class="show-component order-box">
        <UserOrderComp :username="this.username" />
      </div>
      <div id="food-box-container-menu" class="show-component food-boxx">
        <UserFoodComp />
      </div>
      <div id="analysis-box" class="show-component analysis-box">
        <UserAnalysisComp :username="this.username" />
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src

import UserInformationComp from "@/components/UserHomeComp/UserInformationsComp.vue";
import UserOrderComp from "@/components/UserHomeComp/UserOrderComp.vue";
import UserBillComp from "@/components/UserHomeComp/UserBillsComp.vue";
import UserFoodComp from "@/components/UserHomeComp/UserFoodComp.vue";
import UserAnalysisComp from "@/components/UserHomeComp/AdminAnalysisComp.vue";

export default {
  name: "HomeUser",
  data() {
    return {
      username: "",
      hover: false,
    };
  },
  components: {
    UserInformationComp,
    UserOrderComp,
    UserBillComp,
    UserFoodComp,
    UserAnalysisComp,
  },
  methods: {
    logOut() {
      localStorage.removeItem("user-info");
      localStorage.removeItem("admin-info");
      location.reload();
    },
    infoBtn() {
      var billdisplay = document.getElementById("bill-box").style.display;
      var orderdisplay = document.getElementById("order-box").style.display;
      var fooddisplay = document.getElementById("food-box-container-menu").style
        .display;
      var analysisdisplay =
        document.getElementById("analysis-box").style.display;
      if (
        billdisplay ||
        orderdisplay ||
        fooddisplay ||
        analysisdisplay == "block"
      ) {
        document.getElementById("bill-box").style.display = "none";
        document.getElementById("order-box").style.display = "none";
        document.getElementById("analysis-box").style.display = "none";
        document.getElementById("food-box-container-menu").style.display =
          "none";
      }
      //  document.getElementById("info-box").style.display = "block";
      document.getElementById("info-box").style.display = "block";
    },
    billBtn() {
      var infodisplay = document.getElementById("info-box").style.display;
      var orderdisplay = document.getElementById("order-box").style.display;
      var fooddisplay = document.getElementById("food-box-container-menu").style
        .display;
      var analysisdisplay =
        document.getElementById("analysis-box").style.display;
      if (
        infodisplay ||
        orderdisplay ||
        fooddisplay ||
        analysisdisplay == "block"
      ) {
        document.getElementById("info-box").style.display = "none";
        document.getElementById("analysis-box").style.display = "none";
        document.getElementById("order-box").style.display = "none";
        document.getElementById("food-box-container-menu").style.display =
          "none";
      }

      document.getElementById("bill-box").style.display = "block";
    },
    analysisBtn() {
      var infodisplay = document.getElementById("info-box").style.display;
      var billdisplay = document.getElementById("bill-box").style.display;
      var fooddisplay = document.getElementById("food-box-container-menu").style
        .display;

      if (infodisplay || billdisplay || fooddisplay == "block") {
        document.getElementById("info-box").style.display = "none";
        document.getElementById("bill-box").style.display = "none";
        document.getElementById("food-box-container-menu").style.display =
          "none";
        document.getElementById("order-box").style.display = "none";
      }

      document.getElementById("analysis-box").style.display = "block";
    },
    orderBtn() {
      var infodisplay = document.getElementById("info-box").style.display;
      var billdisplay = document.getElementById("bill-box").style.display;
      var fooddisplay = document.getElementById("food-box-container-menu").style
        .display;
      var analysisdisplay =
        document.getElementById("analysis-box").style.display;

      if (
        infodisplay ||
        billdisplay ||
        fooddisplay ||
        analysisdisplay == "block"
      ) {
        document.getElementById("info-box").style.display = "none";
        document.getElementById("bill-box").style.display = "none";
        document.getElementById("food-box-container-menu").style.display =
          "none";
        document.getElementById("analysis-box").style.display = "none";
      }

      document.getElementById("order-box").style.display = "block";
    },
    foodBtn() {
      var infodisplay = document.getElementById("info-box").style.display;
      var billdisplay = document.getElementById("bill-box").style.display;
      var orderdisplay = document.getElementById("order-box").style.display;
      var analysisdisplay =
        document.getElementById("analysis-box").style.display;
      if (
        infodisplay ||
        billdisplay ||
        orderdisplay ||
        analysisdisplay == "block"
      ) {
        document.getElementById("info-box").style.display = "none";
        document.getElementById("bill-box").style.display = "none";
        document.getElementById("analysis-box").style.display = "none";
        document.getElementById("order-box").style.display = "none";
      }

      document.getElementById("food-box-container-menu").style.display =
        "block";
    },
    navShow() {
      document.getElementById("container").classList.toggle("container-change");

      document.getElementById("nav-hover").classList.toggle("nav-show");
      document.getElementById("logout-btn").style.display = "block";
      document.getElementById("logout-btn-change").style.display = "none";
      document.getElementById("orders-icon").style.display = "none";
      document.getElementById("foods-icon").style.display = "none";
      document.getElementById("bills-icon").style.display = "none";
      document.getElementById("analysis-icon").style.display = "none";
      document.getElementById("informations-icon").style.display = "none";
      document.getElementById("bills-title").style.display = "block";
      document.getElementById("analysis-title").style.display = "block";
      document.getElementById("informations-title").style.display = "block";
      document.getElementById("orders-title").style.display = "block";
      document.getElementById("foods-title").style.display = "block";
      document.getElementById("nav-user-name").style.display = "block";
      document.getElementById("analysis-title").style.display = "block";
    },

    navHidden() {
      document.getElementById("nav-hover").classList.replace("nav-show", "nav");
      document
        .getElementById("container")
        .classList.replace("container-change", "container");
      document.getElementById("orders-icon").style.display = "block";
      document.getElementById("foods-icon").style.display = "block";
      document.getElementById("bills-icon").style.display = "block";
      document.getElementById("logout-btn").style.display = "none";
      document.getElementById("logout-btn-change").style.display = "block";
      document.getElementById("informations-icon").style.display = "block";
      document.getElementById("analysis-icon").style.display = "block";
      document.getElementById("bills-title").style.display = "none";
      document.getElementById("analysis-title").style.display = "none";
      document.getElementById("informations-title").style.display = "none";
      document.getElementById("analysis-title").style.display = "none";
      document.getElementById("orders-title").style.display = "none";
      document.getElementById("foods-title").style.display = "none";
      document.getElementById("nav-user-name").style.display = "none";
    },
  },

  mounted() {
    let user = localStorage.getItem("user-info");
    let admin = localStorage.getItem("admin-info");
    //if employer
    if (user) {
      let userString = JSON.parse(user);
      console.log("this is uaer");
      if (userString.status == 200) {
        this.username = userString.data[0].name;
        document.getElementById("analysis-selection").style.display = "none";
        document.getElementById("food-selection").style.display = "none";
        document.getElementById("information-btn").style.display = "block";
        document.getElementById("order-box").style.display = "none";
        document.getElementById("bill-box").style.display = "none";
        document.getElementById("info-box").style.display = "block";
        console.log("found the user", userString);
      } else {
        this.username = userString.data.name;
        console.log("found the user", userString);
      }
    }
    //if admin
    else if (admin) {
      console.log("this is admin");
      let adminString = JSON.parse(admin);
      if (adminString.status == 200) {
        this.username = adminString.data[0].name;
        console.log("found the user", adminString);
      } else {
        this.username = adminString.data.name;
        console.log("found the user", adminString);
      }
      document.getElementById("analysis-selection").style.display = "block";
      document.getElementById("food-selection").style.display = "block";
      document.getElementById("information-btn").style.display = "none";
      document.getElementById("info-box").style.display = "none";
      document.getElementById("bill-box").style.display = "none";
      document.getElementById("food-box-container-menu").style.display = "none";
      document.getElementById("analysis-box").style.display = "block";
    } else {
      this.$router.push({ name: "Home" });
    }
    document
      .getElementById("welcome-text")
      .classList.toggle("welcome-text-released");
    document.getElementById("container").style.top = "10%";
    document.getElementById("container").style.height = "90%";
    setTimeout(() => {
      document.getElementById("container").style.top = "0%";
      document.getElementById("container").style.height = "100%";
    }, 15000);
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
.home-user {
  width: 100%;
  height: 100%;
  background-image: linear-gradient(40deg, $redCol, $whitCol);
  overflow: hidden;
  .welcome-text {
    transition: 0.4s ease-in-out;
    position: absolute;
    top: 0%;
    background: $blueDarkCol;
    height: 10%;
    left: 4%;

    font-family: "Salsa", cursive;
    width: 96%;
    padding-top: 12px;
    font-size: 14px;
    color: $purpleCol;
    letter-spacing: 4px;
    font-weight: 100;
    .user-font-change {
      color: $greenYellCol;
    }
  }
  .welcome-text-released {
    animation: released 1s forwards;
    animation-delay: 15s;
  }
  @keyframes released {
    0% {
      top: 0%;
    }
    100% {
      top: -13%;
    }
  }
  .nav {
    width: 15%;
    height: 100%;
    float: left;

    background: $blueDarkCol;
    margin-left: -10%;
    transition: ease-in-out 0.8s;
    .user-name-box {
      width: 100%;
      height: 10%;
      margin-top: 49%;
    }
    #nav-user-name {
      display: none;
      color: $greenYellCol;
    }
    &::before {
      content: " ";
      height: 0px;
      width: 0px;
      position: absolute;
      top: 10%;
      left: 5%;
      background: #b9827d00;
      z-index: 4;
      border: solid transparent;
      border-width: 17px;
      border-color: #8220;
      border-left-color: $blueDarkCol;
    }
  }
  .nav-show {
    background: $blueDarkCol;
    margin-left: 0%;
    &::before {
      border-width: 0px;
    }
  }

  h3 {
    font-size: 28px;
    font-weight: bolder;
    color: $yellowCol;
  }

  .logout-btn {
    cursor: pointer;
    width: 40%;
    height: 30px;
    display: none;
    border-radius: 10%;
    color: $greenYellCol;
    margin-left: 28%;
    background: none;
    font-weight: bold;
    border: 1px solid $greenYellCol;
  }
  .logout-btn-change {
    margin-left: 0%;
    width: 28%;
    display: block;
    animation: btnchange 1s forwards;
    animation-delay: 0.1s;
  }
  @keyframes btnchange {
    0% {
      margin-left: 0%;
    }
    100% {
      margin-left: 69%;
    }
  }
  .nav-list {
    margin-top: 40%;
    width: 100%;
    height: 50%;
//All Right Reserved B as im Aj ou b
    li {
      width: 100%;
      height: 40px;
      background: $purpleCol;
      color: $greenYellCol;
      margin-bottom: 20px;
      padding-top: 15px;
      cursor: pointer;
//All Right Reserved Basim Ajoub
      a {
        text-decoration: none;
        color: $yellowCol;
        color: $greenYellCol;

        font-size: 20px;
        font-weight: bold;
      }
      .nav-title {
        display: none;
      }

      .list-icon {
        margin-left: 0%;
        width: 20%;
        display: block;
        transition: ease-in-out 0.8s;
        animation: listchange 1s forwards;
        animation-delay: 0.1s;
      }
      @keyframes listchange {
        0% {
          margin-left: 0%;
        }
        100% {
          margin-left: 72%;
        }
      }
    }
    .food-selection {
      display: none;
    }
  }
  .container {
    width: 95%;
    height: 100%;
    //background-image: linear-gradient(40deg, $redCol, $whitCol);
    margin-left: 5%;
    position: absolute;
    top: 10%;
    overflow: hidden;
    transition: ease-in-out 0.8s;
    .show-component {
      width: 93%;
      height: 97%;

      position: absolute;
      top: 2%;
      left: 110%;
      display: none;
      animation: move-left 1s forwards;
      animation-delay: 0.2s;
    }
    .hide-component {
      animation: move-right 1s forwards;
      animation-delay: 0.2s;
    }
    @keyframes move-right {
      0% {
        left: 0%;
      }

      100% {
        left: 110%;
      }
    }
    @keyframes move-left {
      0% {
        left: 110%;
      }

      100% {
        left: 5%;
      }
    }
  }
  .container-change {
    width: 85%;
    margin-left: 15%;
  }
}
#right-title{
  font-size: 10px;
  margin-top:20px;
  margin-left:-65px;
}
</style>
