<template>
  <div class="admin-analysis-comp">
    <div class="comp-title">
      <h1>Analysis</h1>
    </div>
    <div class="infos-form">
      <p id="date-show">Date : <span id="date-now"></span></p>
      <div class="general-user-infos">
        <p>
          Name: <span>{{ username }} .</span>
        </p>
        <p>Type: <span>Admin .</span></p>
      </div>
      <!--Start show user active orders-->
    </div>
    <div class="charts">
      <IncomeYearChart />
    </div>
    <div class="analysis-box">
      <div class="day-box static-box">
        <div class="total-income-today-box">
          <p>Total Income Today</p>
          <h2 id="total-income-today">{{ totalincometoday }} $</h2>
        </div>
      </div>
      <div class="week-box static-box">
        <p>Active Order Now</p>
        <h4 id="active-orders-now">{{ activeordersnow }}</h4>
        <p>Total Bills Today</p>
        <h4 id="total-bills-today">{{ totalbillstoday }}</h4>
      </div>
      <div class="month-box static-box">
        <div class="total-income-month-box">
          <p>Total Income Month</p>
          <h4 id="total-income-month">{{ totalincomemonth }} $</h4>
          <p>Total Bills Month</p>
          <h4 id="total-bills-month">{{ totalbillsmonth }}</h4>
        </div>
      </div>
      <div class="employer-number-box static-box">
        <div class="total-employer-box">
          <p>Total Employer</p>
          <h4 id="total-employer">{{ totalemployer }}</h4>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import IncomeYearChart from "../analysis/IncomeYearChartComp.vue";
import axios from "axios";
export default {
  name: "AdminAnalysisComp",
  components: {
    IncomeYearChart,
  },
  props: ["username"],
  data() {
    return {
      totalincometoday: 0,
      activeordersnow: 0,
      totalbillstoday: 0,
      totalincomemonth: 0,
      totalbillsmonth: 0,
      totalemployer: 0,
    };
  },
  methods: {
    async Employernumber() {
      let resultEmployer = await axios.get("http://localhost:3000/user");
      console.log(resultEmployer.data.length, "true employer number");
      this.totalemployer = resultEmployer.data.length;
    },
    async DateNow() {
      let date = new Date();
      this.activeordersnow = 0;
      this.totalbillstoday = 0;
      this.totalincometoday = 0;
      this.totalincomemonth = 0;
      this.totalbillsmonth = 0;

      document.getElementById("date-now").innerText =
        date.getDate() + "-" + (date.getMonth() + 1) + "-" + date.getFullYear();
      let resultBills = await axios.get("http://localhost:3000/bills");
      let resultOrders = await axios.get("http://localhost:3000/orders");
      let reultbillsdate = resultBills.billdate;

      let nowDay = date.getDate();
      let nowMonth = date.getMonth() + 1;
      let nowYear = date.getFullYear();
      //grt bill and check date comparing with today
      let billsLength = resultBills.data.length;
      for (let i = 0; i < billsLength; i++) {
        let resultbillIncomeToday = resultBills.data[i].totalbill;
        let billdateTimeDiv = resultBills.data[i].billdate.split(" ");
        let billdateDiv = billdateTimeDiv[0].split("/");
        let billday = billdateDiv[0];
        let billmonth = billdateDiv[1];
        let billyear = billdateDiv[2];
        if (billmonth == nowMonth && billyear == nowYear) {
          console.log(billmonth, "true bill year month");
          console.log(this.totalbillstoday, "true day bills");
          let incomeWtSign = resultbillIncomeToday.split("$");
          let incomeToday = Number(incomeWtSign[0]);
          if (billday == nowDay) {
            //total bill today
            this.totalbillstoday += 1;
            this.totalbillsmonth += 1;
            this.totalincometoday += incomeToday;
            this.totalincomemonth += incomeToday;
            console.log(this.totalincometoday, "true day income");
          }
          //bill in this month
          else {
            this.totalincomemonth += incomeToday;
            this.totalbillsmonth += 1;
          }
        }
      }
      //grt order and check date comparing with today
      let ordersLength = resultOrders.data.length;
      for (let j = 0; j < ordersLength; j++) {
        let dateTimeDiv = resultOrders.data[j].billdate.split(" ");
        let dateDiv = dateTimeDiv[0].split("/");
        console.log(dateDiv, dateTimeDiv, "orders", reultbillsdate);
        let day = dateDiv[0];
        let month = dateDiv[1];
        let year = dateDiv[2];
        //check if year and month for bill and order if matching with now date
        //check month static value
        if (month == nowMonth && year == nowYear) {
          console.log(year, month, "true month");
          //check today static value
          if (day == nowDay) {
            //total active orders now
            this.activeordersnow += 1;
          }
        }
      }
    },
  },

  mounted() {
    this.DateNow();
    this.Employernumber();
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
.admin-analysis-comp {
  width: 100%;
  height: 100%;

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
    height: 25%;
    margin-bottom: 6%;
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
    width: 50%;
    height: 50%;
    cursor: pointer;
  }
  .analysis-box {
    width: 40%;
    height: 75%;
    position: absolute;
    left: 58%;
    top: 20%;

    .static-box {
      background: $blueDarkCol;
      border-top-left-radius: 12%;
      border-bottom-right-radius: 12%;
      width: 40%;
      box-sizing: border-box;
      float: left;
      height: 35%;
      cursor: pointer;
      margin-left: 5%;
      margin-bottom: 5%;
      padding-top: 1%;
      .total-employer-box,
      .total-income-month-box {
        width: 100%;
        height: 100%;
      }
      p {
        width: 100%;
        height: 14%;
        color: $greenYellCol;
        margin-top: 12%;
      }
      h4 {
        width: 38%;
        height: 18%;
        background: $purpleCol;
        color: $greenYellCol;
        font-family: "Skranji", cursive;
        border-radius: 90%;
        margin-left: 30%;
        padding-top: 10%;
        text-align: center;
      }
    }
    .month-box,
    .week-box {
      height: 60%;
    }
    .month-box {
      position: absolute;
      top: 35%;
    }
    .employer-number-box {
      margin-left: 50%;
      height: 30%;
      h4 {
        height: 25%;
      }
    }
    .day-box {
      height: 30%;
      background: none;
      p {
        color: $blueDarkCol;
        font-weight: bold;
        font-size: 20px;
      }
      .total-income-today-box {
        width: 100%;
        height: 100%;
        h2 {
          background: $purpleCol;
          color: $blueDarkCol;
          font-size: 22px;
          padding-top: 10%;
          width: 100%;
          margin-left: 0%;
          font-family: "Luckiest Guy", cursive;
        }
      }
    }
  }
  #date-show {
    color: $blueDarkCol;
    margin-left: 55%;
  }
}
</style>
