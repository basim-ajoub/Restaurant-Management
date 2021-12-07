<template>
  <div class="user-bills-comp">
    <div class="comp-title">
      <h1>Bills</h1>
    </div>
    <div class="bill-table">
      <table>
        <tr class="main-row">
          <th>No.</th>
          <th>Bill</th>
          <th>Amount</th>
          <th>Date</th>
          <th>Table No.</th>
          <th>Employer</th>
          <th>Branch</th>
        </tr>
        <tr v-for="bill in bills" :key="bill.key" class="secandry-row">
          <td>{{ bill.id }}</td>
          <td>{{ bill.billnumber }}</td>
          <td>{{ bill.totalbill }}</td>
          <td>{{ bill.billdate }}</td>
          <td>{{ bill.tablenumber }}</td>
          <td>{{ bill.employername }}</td>
          <td>Berlin</td>
        </tr>
      </table>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "UserBillsComp",
  data() {
    return {
      username: "",
      bills: {
        employername: "",
        tablenumber: "",
        billdate: "",
        totalbill: "",
        billnumber: "1",
        id: "",
      },
    };
  },
  mounted() {
    this.showOrders();
  },

  methods: {
    async showOrders() {
      let user = localStorage.getItem("user-info");
      let admin = localStorage.getItem("admin-info");
      //if employer
      if (user) {
        let userString = JSON.parse(user);
        this.username = userString.data[0].name;
        let result = await axios.get(
          "http://localhost:3000/bills?employername=" + this.username
        );

        this.bills = result.data;
        console.log(this.bills);
      }
      //if admin
      else if (admin) {
        //   this.username = userString.data[0].name;
        let result = await axios.get("http://localhost:3000/bills");
        this.bills = result.data;
        console.log(result.data);
      }
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
.user-bills-comp {
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
  .bill-table {
    width: 100%;
    height: 80%;
    overflow-y: scroll;
    td {
      width: 10%;
      button {
        cursor: pointer;
        width: 40%;
        height: 20px;
        margin-left: 2%;
        padding: 2px 2px 2px 2px;
        background-image: linear-gradient(89deg, #ff7854, #ffaf48);
        border: 0px;
        color: $yellowCol;
        border-radius: 10%;
      }
    }
    table {
      width: 100%;

      .secandry-row {
        height: 45px;
        color: $blueDarkCol;
        font-weight: bold;
        transition: 0.2s ease-in-out;
        cursor: pointer;
        &:hover {
          background: $greenYellCol;
          border: 1px solid $purpleCol;
        }
        td:hover {
          border: 1px solid $blueDarkCol;
          background: $purpleCol;
          color: $greenYellCol;
        }
      }
      .main-row {
        height: 60px;
        background: $blueDarkCol;
        color: $greenYellCol;
        th {
          border-radius: 5%;
        }
      }
    }
  }
}
</style>
