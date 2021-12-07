<template>
  <div class="income-year-chart-comp">
    <div class="chart-year-box">
      <apexchart
        id="area-chart"
        type="area"
        width="600"
        height="290"
        :options="chartOptions"
        :series="series"
      ></apexchart>
    </div>
  </div>
</template>
<script>
import VueApexCharts from "vue3-apexcharts";
import axios from "axios";
export default {
  name: "IncomeChartComp",
  components: {
    apexchart: VueApexCharts,
  },
  data: function () {
    return {
      //to add new chart change the code bootom and code in templte only
      //to add new chart change the code from here keep return and data function and code in templte only

      series: [
        {
          name: "Total Income",
          data: [],
        },
      ],
      chartOptions: {
        title: {
          text: "Total Income / Year",
          align: "left",
          style:{
            color:"#111324",
               fontFamily: "Salsa,cursive",
             
              fontWeight: "bold",
              fontSize: "16px",

          },
        },
        theme: {
          mode: "light",
          palette: "palette1",
          monochrome: {
            enabled: true,
            color: "#111324",
            shadeTo: "light",
            shadeIntensity: 0.65,
          },
        },
        fill: {
          colors: ["#7856ff"],
          opacity: 0.5,
          type: "solid",
          gradient: {
            shade: "dark",
            type: "horizontal",
            shadeIntensity: 0.9,
            gradientToColors: ["#cdd400"],
          },
        }, //to change pie color
        markers: { colors: ["#cdd400"] },
        chart: {
          height: 290,
          type: "area",
        },
        dataLabels: {
          enabled: false,
        },
        stroke: {
          curve: "smooth",
        },
        xaxis: {
          type: "datetime",
          // categories: [""],

          categories: [],
        },
        tooltip: {
          x: {
            format: "dd/MM/yy HH:mm",
          },
        },
      },

      //end return
    };
  },
  mounted() {
    this.dailyChart();
  },
  methods: {
    async dailyChart() {
      this.series[0].data = [null];
      let result = await axios.get("http://localhost:3000/bills");
      console.log(result.data.length, "chart result value");
      for (let i = 0; i <= result.data.length - 1; i++) {
        var stringSingleTotalBill = result.data[i].totalbill.split("$");
        var singleTotalBill = Number(stringSingleTotalBill[0]);
        this.series[0].data[i] = singleTotalBill;
        //time and date
        //we should conver time and date tothis form 2018-09-19T01:30:00.000Z
        var stringDateAndTime = result.data[i].billdate.split(" ");
        var completeDate = stringDateAndTime[0];
        var completeTime = stringDateAndTime[1];
        //change date formate
        var dividcompleteDate = completeDate.split("/");
        var day = dividcompleteDate[0];
        var month = dividcompleteDate[1];
        var year = dividcompleteDate[2];
        var finalDateForm = year + "-" + month + "-" + day;
        //we should conver time and date tothis form 2018-09-19T01:30:00.000Z
        var dateAndTime = finalDateForm + "T" + completeTime + ".000Z";
        this.chartOptions.xaxis.categories[i] = dateAndTime;
      }
      console.log(this.series[0].data, "chart series");
    },
  },
};
</script>
<style lang="scss">
.income-year-chart-comp {
  width: 100%;
 
  height: 100%;
  .chart-year-box {
    width: 100%;
    height: 90%;
  }
}
 .apexcharts-tooltip {
    font-family: "Salsa,cursive";
font-weight: bold;
    color: #111324;
  }
</style>
