<template>
  <div class="user-information-comp">
    <div class="comp-title">
      <h1>Informations</h1>
    </div>
    <div class="infos-form">
      <div class="general-user-infos">
        <p>
          Name: <span id="user-name-field">{{ username }}</span>
        </p>
        <p>Type: <span>Employer .</span></p>
      </div>
      <!--Start show user active orders-->
      <div class="user-activ-orders">
        <p>
          Active Order : <span id="get-employer-orders">12</span> /
          <span id="get-all-employer-orders">12</span>
        </p>
      </div>
      <!--Start show user bills-->
      <div class="user-bills">
        <p>
          Bills Confirmed : <span id="get-employer-bills">14</span> /
          <span id="get-all-employer-bills"></span>
        </p>
      </div>
    </div>
    <div class="charts">
      <infoChartsComp />
    </div>
  </div>
</template>
<script>
import infoChartsComp from "../information/InfoChartComp.vue";
export default {
  name: "UserInfosComp",
  props: {
    username: String,
  },
  components: {
    infoChartsComp,
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
.user-information-comp {
  width: 100%;
  height: 100%;
  //background: red;
  position: relative;
  .comp-title {
    width: 100%;
    height: 20%;

    h1 {
      margin-top: -3.5%;

      font-size: 50px;
      letter-spacing: 0.1em;
      -webkit-text-fill-color: transparent;
      -webkit-text-stroke-width: 3px;
      -webkit-text-stroke-color: $blueDarkCol;
      text-shadow: 8px 8px $purpleCol;
      font-weight: normal;
      font-family: "Bungee Inline", cursive;
    }
  }
  .infos-form {
    width: 100%;
    height: 35%;

    .general-user-infos {
      width: 100%;
      height: 60%;
      position: relative;
      text-align: left;
      box-sizing: border-box;
      padding-top: 5%;

      p {
        margin-bottom: 2%;
        margin-right: 10%;
        font-weight: bolder;
        font-size: 19px;
        color: $blueDarkCol;
        font-family: "Salsa,cursive";
        span {
          margin-left: 2%;
          font-weight: bold;
          font-size: 18px;
          color: $purpleCol;
        }
      }
    }
    .user-activ-orders {
      width: 15%;
      height: 5%;
      bottom: 0;

      left: 23%;
      position: absolute;
      font-family: "Salsa,cursive";
      font-weight: bolder;
      font-size: 14px;
      color: $blueDarkCol;
    }
    .user-bills {
      width: 15%;
      height: 5%;
      bottom: 0;
      left: 85%;
      position: absolute;

      font-weight: bolder;
      font-size: 14px;
      color: $blueDarkCol;
      font-family: "Salsa,cursive";
    }
  }
  .charts {
    width: 100%;
    margin-top: 1%;
    height: 43%;
    // background: orange;
    cursor: pointer;
  }
}
</style>
