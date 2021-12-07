<template>
  <div class="o-boxx">
    <div class="table-number">
      <p>Table No.</p>
      <a href="#">{{ tablenumber }}</a>
    </div>
    <div class="order-bill">
      <p>
        Bill No. : <span id="copy-bill-number">{{ billnumber }}</span>
      </p>
      <p>
        Date: <span>{{ billdate }}</span>
      </p>
      <p>
        Employer : <span>{{ employername }}</span>
      </p>
      <p>
        Total : <span>{{ totalbill }}</span>
      </p>
    </div>
    <div :id="'edit-btn-box' + this.billnumber" class="edit-order-btn-list">
      <button @click="showDeleteMessage" id="show-delte-page-btn">
        Delete
      </button>
      <button @click="requestBill" id="bill-btnn">Bill</button>
    </div>
    <div
      :id="'delete-message-box' + this.billnumber"
      class="edit-order-btn-list delete-message-box"
    >
      <p>Delete This Order</p>
      <button @click="cancellDeletingOrder">Cancel</button>
      <button @click="deleteOrder" id="show-delte-page-btn">Delete</button>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "boxOrderr",
  props: [
    "billnumber",
    "tablenumber",
    "type",
    "totalbill",
    "billdate",
    "employername",
    "orderid",
    "method",
  ],

  methods: {
    async requestBill() {
      let result = await axios.post("http://localhost:3000/bills", {
        employername: this.employername,
        tablenumber: this.tablenumber,
        billnumber: this.billnumber,
        billdate: this.billdate,
        totalbill: this.totalbill,
      });
      if (result.status == 201) {
        await axios.delete("http://localhost:3000/orders/" + this.orderid);
        this.method();
        location.reload();
      }
    },
    showDeleteMessage() {
      document.getElementById("edit-btn-box" + this.billnumber).style.display =
        "none";
      document.getElementById(
        "delete-message-box" + this.billnumber
      ).style.display = "block";
    },
    async deleteOrder() {
      await axios.delete("http://localhost:3000/orders/" + this.orderid);
      this.method();
    },
    cancellDeletingOrder() {
      document.getElementById(
        "delete-message-box" + this.billnumber
      ).style.display = "none";
      document.getElementById("edit-btn-box" + this.billnumber).style.display =
        "block";
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
.o-boxx {
  width: 20%;
  height: 48%;
  float: left;
  background: $blueDarkCol;
  padding-top: 1%;
  box-sizing: border-box;
  border-top-right-radius: 10%;
  border-top-left-radius: 10%;
  z-index: 100;
  border-bottom-right-radius: 10%;
  margin-left: 4%;
  color: $greenYellCol;
  margin-bottom: 3%;

  .table-number {
    width: 95%;
    margin-left: 2.5%;
    height: 35%;
    background: $purpleCol;
    margin-bottom: 8%;
    position: relative;
    box-sizing: border-box;
    border-top-right-radius: 10%;
    border-top-left-radius: 10%;
    padding: 11px 30px 20px 5px;
    p {
      color: $blueDarkCol;
      font-size: 13px;
      text-align: left;
      letter-spacing: 0.5px;
    }
    a {
      font-size: 50px;
      text-decoration: none;
      color: $greenYellCol;
      position: absolute;
      margin-top: -8.5%;
      font-family: "Skranji", cursive;
    }
  }
  .order-bill {
    width: 100%;
    height: 38%;
    p {
      color: $purpleCol;
      margin-top: 1%;
      font-size: 14px;
      font-family: "Salsa", cursive;
      span {
        color: $greenYellCol;
      }
    }
  }

  .edit-order-btn-list {
    width: 100%;
    height: 14%;
    border-bottom-right-radius: 8%;
    display: block;
    button {
      width: 30%;
      margin-left: 1.5%;
      height: 60%;
      color: $blueDarkCol;
      &:hover {
        border-bottom: 1px solid $greenYellCol;
        border-left: 1px solid $greenYellCol;
      }
    }
  }
  .delete-message-box {
    display: none;
  }
}
</style>
