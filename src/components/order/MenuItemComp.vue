<template>
  <div class="item-box-comp">
    <div id="food-box" class="food-box">
      <div class="icon-box">
        <i class="fas fa-utensils icon"></i>
      </div>
      <ul>
        <li>
          <p>Name :</p>
          <span id="show-food-name">{{ this.itemmenuName }}</span>
        </li>
        <li>
          <p>Type :</p>
          <span id="show-food-type">{{ this.itemmenuType }}</span>
        </li>
        <li>
          <p>Price :</p>
          <span id="show-food-price">{{ this.itemmenuPrice }} $</span>
        </li>
        <li class="btn-list">
          <input
            :id="'show-food-quantity-' + itemmenuName"
            type="number"
            value="1"
          /><button @click="AddBtn" id="menu-item-edit">Add</button>
        </li>
      </ul>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "MenuItemComp",
  data() {
    return {
      edititemtype: "",
    };
  },
  props: ["itemmenuName", "itemmenuType", "itemmenuPrice"],
  methods: {
    AddBtn() {
      let numberOfOrder = document.getElementById("table").rows.length;
      console.log("order row number ", this.itemmenuType);
      // let selctedItemName =  document.getElementById("show-food-name").innerText;
      //    let selctedItemType =  document.getElementById("show-food-type").innerText;
      let selctedItemQuantity = document.getElementById(
        "show-food-quantity-" + this.itemmenuName
      ).value;
      //   let selctedItemPrice =  document.getElementById("show-food-price").innerText;
      //to take only price number without $ sign
      //   let divPrice = this.itemmenuPrice.split("$");
      //convert to number
      //  let selctedItemPriceInNumber = Number(divPrice[0]);
      //total price = quantity * item price
      let selctedItemTotalPrice = this.itemmenuPrice * selctedItemQuantity;

      document.getElementById("table").innerHTML +=
        '<tr class="secandry-row"><td id="' +
        numberOfOrder +
        '" class="row1">' +
        numberOfOrder +
        '</td><td id="item-1" class="row3">' +
        this.itemmenuName +
        '</td><td id="type-1" class="row2">' +
        this.itemmenuType +
        '</td><td id="price-1" class="row2">' +
        this.itemmenuPrice +
        ' $</td><td id="quantity-1" class="row1">' +
        selctedItemQuantity +
        '</td><td id="total-1" class="row2">' +
        selctedItemTotalPrice +
        " $</td></tr>";
      //total bill Sum
      let textTotalBillSum = document.getElementById("total-bill").innerText;
      //to take only price number without $ sign
      let divTotalBillSum = textTotalBillSum.split("$");
      //convert to number
      let TotalBillSum = Number(divTotalBillSum[0]);
      document.getElementById("total-bill").innerText =
        Number(TotalBillSum) + selctedItemTotalPrice + "  $";
    },
    async DeleteBtn() {
      await axios.delete("http://localhost:3000/menu/" + this.itemid);
      location.reload();
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
.item-box-comp {
  width: 100%;
  position: relative;
  height: 100%;

  .food-box {
    width: 100%;
    height: 100%;
    position: relative;
    padding-top: 25px;
    .icon-box {
      width: 60%;
      height: 40%;
      border-top-right-radius: 15%;
      background: $greenYellCol;

      .icon {
        width: 70%;
        height: 70%;
        color: $greenYellCol;
        margin-top: 8%;
        margin-right: 20%;
        font-size: 14px;
        color: $purpleCol;
      }
    }
    ul {
      width: 100%;
      height: 58%;
      padding-top: 5%;
      list-style-type: none;
      padding-left: 3px;
      text-align: left;
      background: $purpleCol;
      border-bottom-right-radius: 5%;
      border-bottom-left-radius: 5%;
      li {
        font-size: 12px;

        p {
          float: left;
          color: $blueDarkCol;
        }
        span {
          margin-left: 1px;
          color: $greenYellCol;
        }
        button {
          width: 40%;
          height: 100%;
          margin-left: 7%;
          background: $blueDarkCol;
          font-size: 11px;
          color: $greenYellCol;
          border: 0.5px;
          cursor: pointer;
        }
      }
      .btn-list {
        margin-top: 4%;
        input {
          margin-left: 2%;
          width: 35%;
          height: 80%;
          background: $greenYellCol;
          color: $blueDarkCol;
          border: 1px;
          padding-left: 1px;
        }
      }
    }
  }
}
</style>
