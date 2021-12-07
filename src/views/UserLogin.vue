<template>
  <div class="about">
    <div id="signupbox" class="signup log-box">
      <SigUpComp />
    </div>
    <div id="loginbox" class="login log-box">
      <LogInComp />
    </div>
  </div>
</template>

<script>
import SigUpComp from "../components/login/SignUpComp.vue";
import LogInComp from "../components/login/LogInComp.vue";
export default {
  name: "LogView",
  components: {
    SigUpComp,
    LogInComp,
  },
  methods: {},
};
</script>

<style lang="scss">
$blueCol: #024566;
$yellowCol: #f5d9a6;
$redCol: #b37a79;
.about {
  width: 100%;
  height: 89%;
  padding-top: 5%;

  .log-box {
    margin-left: 33%;
    width: 30%;
    height: 90%;
    z-index: 2;
    position: relative;
    background: $redCol;
    color: $blueCol;
    border-radius: 1%;
    border-top-left-radius: 15%;
    border-bottom-right-radius: 15%;
    padding-top: 10px;
  }
  #signupbox {
    display: none;
  }
  #loginbox {
    display: block;
  }
}
</style>
