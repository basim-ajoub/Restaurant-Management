<template>
  <div class="charts-comp">
    <div class="pie-chart-container">
      <div class="orders-pie-chart-box">
        <apexchart
          class="pie-chart"
          type="donut"
          :options="orderspie.chartOptions"
          :series="orderspie.series"
        ></apexchart>
      </div>
      <div class="bills-pie-chart-box">
        <apexchart
          class="pie-chart"
          type="donut"
          :options="billspie.chartOptions"
          :series="billspie.series"
        ></apexchart>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";
import VueApexCharts from "vue3-apexcharts";
export default {
  name: "infoChartsComp",
  components: {
    apexchart: VueApexCharts,
  },
  data() {
    return {
      username: "",
      orderspie: {
        series: [null],
        chartOptions: {
          labels: [null],
          colors: ["#cdd400", "#7856ff"], //to change labels color
          fill: { colors: ["#cdd400", "#7856ff"] }, //to change pie color
          title: {
            //pie title
            text: "Your Active Orders Now", //change pie title information and setting
            align: "left",
            style: {
              //change title style
              color: "#111324",
              fontFamily: "Salsa,cursive",
              stroke: "#7884c100",
              fontWeight: "bold",
              fontSize: "16px",
            },
          },

          chart: {
            type: "donut",
          },
          responsive: [
            {
              breakpoint: 480,
              options: {
                chart: {
                  width: 10,
                },
                legend: {
                  position: "bottom",
                },
              },
            },
          ],
        },
      },

      billspie: {
        series: [null],
        chartOptions: {
          labels: [null],
          colors: ["#cdd400", "#7856ff"], //to change labels color
          fill: { colors: ["#cdd400", "#7856ff"] }, //to change pie color
          title: {
            text: "Your Bills", //change pie title information and setting
            align: "left",
            style: {
              //change title style
              color: "#111324",
              fontFamily: "Salsa,cursive",
              stroke: "#7884c100",
              fontWeight: "bold",
              fontSize: "16px",
            },
          },
          //to change datalabel setting

          chart: {
            type: "donut",
            width: "40%",
          },

          responsive: [
            {
              breakpoint: 480,
              options: {
                chart: {
                  width: "20%",
                },
                legend: {
                  position: "bottom",
                },
              },
            },
          ],
        },
      },
    };
  },
  async mounted() {
    await this.countActiveOrderPerEmployer();
    await this.countBillPerEmployer();
  },
  methods: {
    // count how many active order for this employer
    async countActiveOrderPerEmployer() {
      //we can get the user name buy two ways here is one way by localstorage and next data getting by 2nd way
      let getnamefromlocal = JSON.parse(localStorage.getItem("user-info"))
        .data[0].name;

      let result = await axios.get(
        "http://localhost:3000/orders/?employername=" + getnamefromlocal
      );
      //number of active order for this employer
      var separateResult = result.data.length;
      this.orderspie.series[0] = separateResult;

      this.orderspie.chartOptions.labels[0] = "Your Active Order";
      document.getElementById("get-employer-orders").innerText = separateResult;
      //all active order now in restaurants
      let allResult = await axios.get("http://localhost:3000/orders");
      this.orderspie.series[1] = allResult.data.length;
      document.getElementById("get-all-employer-orders").innerText =
        allResult.data.length;
      this.orderspie.chartOptions.labels[1] = ["Restaurant Orders"];
      //this.style.colors = "red";

      //    this.showorders = { singleorder: result.data };
    },

    // count how many bills for this employer amoung all employers in the restaurant
    async countBillPerEmployer() {
      var userName = document.getElementById("user-name-field").innerText;

      let result = await axios.get(
        " http://localhost:3000/bills/?employername=" + userName
      );
      //number of active order for this employer
      var separateResult = result.data.length;

      this.billspie.series[0] = separateResult;
      document.getElementById("get-employer-bills").innerText = separateResult;
      this.billspie.chartOptions.labels[0] = "Your Bills";

      //all active order now in restaurants
      let allResult = await axios.get(" http://localhost:3000/bills");
      this.billspie.series[1] = allResult.data.length;
      document.getElementById("get-all-employer-bills").innerText =
        allResult.data.length;
      this.billspie.chartOptions.labels[1] = ["Restaurant Bills"];

      console.log(separateResult);
      //    this.showorders = { singleorder: result.data };
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
.charts-comp {
  width: 93%;
  height: 100%;
  .pie-chart-container {
    // background: rgb(186, 228, 186);
    width: 100%;
    height: 100%;
  }
  .orders-pie-chart-box {
    width: 40%;
    height: 100%;
    float: left;
    //  background: blue;
  }
  .bills-pie-chart-box {
    width: 40%;
    height: 60%;
    //  background: red;
    margin-left: 60%;
  }
  .pie-chart {
    transition: ease-in-out 0.4s;
    color: $blueCol;
  }
}
</style>
