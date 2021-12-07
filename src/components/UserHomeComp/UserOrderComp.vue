<template>
  <div class="user-orders-comp">
    <div class="comp-title">
      <h1>Orders</h1>
    </div>
    <div class="order-btns">
      <button @click="onGoingOrder">On Going Orders</button>
      <button @click="newOrder" id="new-order-btn">New</button>
    </div>
    <div id="edit-order-box" class="edit-order-box">
      <orderrBoxx
        v-for="order in showorders"
        :key="order.key"
        :method="onGoingOrder"
        :totalbill="order.totalbill"
        :billdate="order.billdate"
        :type="order.type"
        :billnumber="order.billnumber"
        :tablenumber="order.tablenumber"
        :employername="order.employername"
        :orderid="order.id"
      />
    </div>
    <div id="order-box-disc" class="order-box-disc">
      <div class="menu-list">
        <div class="menu-nav">
          <ul>
            <li>
              <span @click="foodsList" class="foods-btn item-btn">Foods</span>
              <select name="foods-list" id="foods-list">
                <option value="pizza-foods">Pizza</option>
                <option value="sandwish-foods">Sandwish</option>
                <option value="meal-foods">Meal</option>
              </select>
            </li>

            <li>
              <span @click="drinksList" class="drinks-btn item-btn">
                Drinks</span
              >
              <select name="drinks-list" id="drinks-list">
                <option value="cold-drinks">Cold Drinks</option>
                <option value="hot-drinks">Hot Drinks</option>
                <option value="alkohol-drinks">Alkohol Drinks</option>
              </select>
            </li>

            <li>
              <span @click="sweetsList" class="sweets-btn item-btn">
                Sweet</span
              >
              <select name="sweets-list" id="sweet-list">
                <option value="brownie">Brownie</option>
                <option value="cookie">Cookie</option>
              </select>
            </li>
          </ul>
        </div>
        <div class="menu-items">
          <div id="foods-menu" class="foods-menu item-menu">
            <div class="menu-container item-menu food-box">
              <MenuItemComp
                v-for="fooditem in menufooditems"
                :key="fooditem.key"
                :itemmenuName="fooditem.name"
                :itemmenuPrice="fooditem.price"
                :itemmenuType="fooditem.type"
                class="item"
              />
            </div>
          </div>
          <div id="drinks-menu" class="drinks-menu item-menu">
            <div class="menu-container item-menu drink-box">
              <MenuItemComp
                v-for="drinkitem in menudrinkitems"
                :key="drinkitem.key"
                :itemmenuName="drinkitem.name"
                :itemmenuPrice="drinkitem.price"
                :itemmenuType="drinkitem.type"
                class="item"
              />
            </div>
          </div>
          <div id="sweets-menu" class="sweets-menu item-menu">
            <div class="menu-container item-menu drink-box">
              <MenuItemComp
                v-for="sweetitem in menusweetitems"
                :key="sweetitem.key"
                :itemmenuName="sweetitem.name"
                :itemmenuPrice="sweetitem.price"
                :itemmenuType="sweetitem.type"
                class="item"
              />
            </div>
          </div>
        </div>
      </div>
      <div class="customer-order">
        <div class="order-main-info">
          <div class="restaurant-info">
            <h3>Ajjoub Restaurant</h3>

            <h5>{{ username }}</h5>
          </div>
          <div class="order-date">
            <ul>
              <li class="bill-no">
                Bill No:<span id="bill-random-number"> 12552</span>
              </li>
              <li>
                Table No:
                <span id="table-number-field">
                  <input id="table-number" width="10px" type="number" value="0"
                /></span>
              </li>
              <li class="date">
                Date: <span id="date-time-now"> 14-10-2021</span>
              </li>
            </ul>
          </div>
        </div>
        <div class="order-list">
          <div class="table-order">
            <table id="table">
              <tr class="main-row">
                <th class="row1">No.</th>
                <th class="row3">Order</th>
                <th class="row2">Type</th>
                <th class="row2">Price</th>
                <th class="row1">Quantity</th>
                <th class="row2">Total</th>
              </tr>
            </table>
          </div>
          <div class="total-bill">
            <p>Total : <span id="total-bill">0 $</span></p>
            <button @click="makeOrder">Order</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import orderrBoxx from "../order/OrderBoxComp.vue";
import MenuItemComp from "../order/MenuItemComp.vue";
import axios from "axios";

export default {
  name: "userOrdersComp",
  components: {
    orderrBoxx,
    MenuItemComp,
  },
  props: ["username"],

  data() {
    return {
      menufooditems: {},
      menudrinkitems: {},
      menusweetitems: {},
      bill: "",
      orders: {
        no: [],
        type: [],
        item: [],
        price: [],
        quantity: [],
        totalprice: [],
      },
      showorders: {},
    };
  },
  mounted() {
    this.onGoingOrder();
    this.showFoodMenu();
    this.showDrinkMenu();
    this.showSweetMenu();
  },
  methods: {
    async showFoodMenu() {
      let itemMenu = await axios.get("http://localhost:3000/menu?type=food");

      this.menufooditems = itemMenu.data;
      console.log(this.menufooditems, "menu items");
    },
    async showDrinkMenu() {
      let itemMenu = await axios.get("http://localhost:3000/menu?type=drink");

      this.menudrinkitems = itemMenu.data;
      console.log(this.menudrinkitems, "menu items");
    },
    async showSweetMenu() {
      let itemMenu = await axios.get("http://localhost:3000/menu?type=sweet");

      this.menusweetitems = itemMenu.data;
      console.log(this.menusweetitems, "menu items");
    },
    foodsList() {
      document.getElementById("sweets-menu").style.display = "none";
      document.getElementById("drinks-menu").style.display = "none";
      document.getElementById("foods-menu").style.display = "block";
    },
    drinksList() {
      console.log("drink pressed");
      document.getElementById("foods-menu").style.display = "none";
      document.getElementById("sweets-menu").style.display = "none";
      document.getElementById("drinks-menu").style.display = "block";
    },
    sweetsList() {
      document.getElementById("foods-menu").style.display = "none";
      document.getElementById("drinks-menu").style.display = "none";
      document.getElementById("sweets-menu").style.display = "block";
    },
    newOrder() {
      console.log("new order pressed");
      document.getElementById("order-box-disc").style.display = "flex";
      document.getElementById("edit-order-box").style.display = "none";
      //Start get date

      var today = new Date();
      // or    var GermanTime = today.toLocaleTimeString();
      var dd = String(today.getDate()).padStart(2, "0");
      var mm = String(today.getMonth() + 1).padStart(2, "0");
      var yyyy = today.getFullYear();
      var GermanTime = today.toTimeString();
      var splitGermanTime = GermanTime.split(" "); //to get only time in 24hour
      //for time in 12 hour
      //var GermanTime = today.toLocaleTimeString();

      today = dd + "/" + mm + "/" + yyyy;
      console.log(splitGermanTime[0]); //edit to change
      document.getElementById("date-time-now").innerText =
        today + " " + splitGermanTime[0];
      //End get date

      //start get random uniq bill number
      var randomNumber = Math.random() * 100000000000000000;
      document.getElementById("bill-random-number").innerText = randomNumber;

      //end get random bill number
    },
    //start show live orders functions
    async onGoingOrder() {
      document.getElementById("order-box-disc").style.display = "none";
      document.getElementById("edit-order-box").style.display = "block";
      //to check if the user admin or employer
      //if employer
      // let  UserlocalStorage =
      if (localStorage.getItem("user-info") != null) {
        // to check in local storage the user name to get only orders for this user

        let getUserNameGroup = localStorage.getItem("user-info");
        let getStringEmployerName = JSON.parse(getUserNameGroup);

        var employername = getStringEmployerName.data[0].name;

        let result = await axios.get(
          " http://localhost:3000/orders/?employername=" + employername
        );

        //number of orders by geting length of sreies of orders number
        //var ordersNumber = result.data.length;
        //loop on database orders to get all orders and arrange each order in onebox
        this.showorders = result.data;
      }
      //if admin
      //  let AdminlocalStorage = localStorage.getItem("admin-info");
      else if (localStorage.getItem("admin-info") != null) {
        console.log("found admin");
        let result = await axios.get("http://localhost:3000/orders");

        console.log("adminnn", result.data);
        this.showorders = result.data;
      }
      //end show live orders functions
      else {
        console.log("erorr while geting Order");
      }
      //start make bill for order functions
    },
    async makeOrder() {
      var count = -1;

      var table = document.getElementById("table");
      //calculate number of rows in table and excluding first row [i=0]
      for (let i = 1; i < table.rows.length; i++) {
        //separate each row in table

        var singleRow = table.rows[i];

        console.log("count" + count);
        //calculate number of cells in each row
        console.log(singleRow.cells.length);
        count++;
        const value = [null];
        for (let j = 0; j < singleRow.cells.length; j++) {
          var singleCell = singleRow.cells[j];
          var getCellContent = singleCell.innerHTML;

          value[j] = getCellContent;
        }
        this.orders.no[count] = value[0];
        this.orders.item[count] = value[1];
        this.orders.type[count] = value[2];
        this.orders.price[count] = value[3];
        this.orders.quantity[count] = value[4];
        this.orders.totalprice[count] = value[5];
        console.log(this.orders);
      }
      var tableNumber = document.getElementById("table-number").value;
      var billNumber = document.getElementById("bill-random-number").innerText;
      var billDate = document.getElementById("date-time-now").innerText;
      var totalBill = document.getElementById("total-bill").innerText;
      let result = await axios.post("http://localhost:3000/orders", {
        employername: this.username,
        customerorder: this.orders,
        tablenumber: tableNumber,
        billnumber: billNumber,
        billdate: billDate,
        totalbill: totalBill,
      });
      console.log("result" + result.status);
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
.user-orders-comp {
  width: 100%;
  height: 100%;
  // background: wheat;
  color: black;
  button {
    border: none;
    border-radius: 12%;
    //background-image: linear-gradient(40deg, $purpleCol, $whitCol, $purpleCol);
    background: $purpleCol;
    cursor: pointer;
    color: $greenYellCol;
    border-bottom: 2px solid $blueDarkCol;
    border-left: 2px solid $blueDarkCol;
    font-family: "Salsa", cursive;
  }
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
  .order-btns {
    width: 100%;
    height: 5%;
    display: flex;
    justify-content: flex-start;

    box-sizing: border-box;
    padding-left: 3%;
    button {
      width: 10%;
      height: 99.8%;
      margin-left: 2%;
      background: $blueDarkCol;
      border-bottom: 2px solid $purpleCol;
      border-left: 2px solid $purpleCol;
      font-size: 12px;
    }
  }
  .edit-order-box {
    width: 99%;
    height: 81%;
    display: none;
    //background: red;
    margin-top: 0.45%;
    box-sizing: border-box;
    overflow: hidden;
    overflow-y: scroll;
    padding: 20px 15px 20px 15px;

    .comp-boxx {
      width: 100%;
      height: 50%;
    }
  }
  .order-box-disc {
    width: 100%;
    height: 82%;

    display: flex;
    display: none;
    .menu-list {
      width: 59%;
      height: 100%;

      .menu-nav {
        width: 100%;
        height: 10%;

        ul {
          list-style: none;
          box-sizing: border-box;
          margin-left: 5%;
          padding-top: 2%;
          width: 100%;
          li {
            width: 30%;
            float: left;
            select {
              margin-left: 5%;
              width: 60%;
              background: $greenYellCol;
              color: $blueDarkCol;
              font-family: "Salsa", cursive;
              border: 1px;
            }
            .item-btn {
              cursor: pointer;
              padding: 3px 5px 5px 3px;
              border-radius: 10%;
              font-family: "Salsa", cursive;
              background: $purpleCol;
              font-size: 14px;
              transition: 0.4s ease-in-out;
              color: $blueDarkCol;
              &:hover {
                background: $greenYellCol;
                border: 0.5px solid $purpleCol;
              }
            }
          }
        }
      }
      .menu-items {
        width: 98%;
        height: 86%;

        .item-menu {
          width: 57.8%;
          position: absolute;
          height: 70%;
          border-radius: 5%;
          font-family: "Salsa", cursive;
          .item {
            width: 20%;
            height: 35%;
            float: left;
            margin-left: 4%;
            margin-bottom: 4%;
          }
        }
        .menu-container {
          width: 95%;
          height: 94%;
          margin-top: 2.5%;
          margin-left: 2.5%;

          overflow-y: scroll;
          border-radius: 0%;
        }
        .foods-menu {
          background: $blueDarkCol;
          display: block;
          &::before {
            content: " ";
            height: 0px;
            width: 0%;
            position: absolute;
            top: -33px;
            left: 8%;
            background: #b9827d00;
            z-index: 4;
            border: solid transparent;
            border-width: 17px;
            border-color: #8220;
            border-bottom-color: $blueDarkCol;
          }
        }

        .drinks-menu {
          background: $blueDarkCol;
          display: none;
          &::before {
            content: " ";
            height: 0px;
            width: 0%;
            position: absolute;
            top: -33px;
            left: 38.5%;
            background: #b9827d00;
            z-index: 4;
            border: solid transparent;
            border-width: 17px;
            border-color: #8220;
            border-bottom-color: $blueDarkCol;
          }
        }

        .sweets-menu {
          background: $blueDarkCol;
          display: none;
          &::before {
            content: " ";
            height: 0px;
            width: 0%;
            position: absolute;
            top: -33px;
            left: 69.5%;
            background: #b9827d00;
            z-index: 4;
            border: solid transparent;
            border-width: 17px;
            border-color: #8220;
            border-bottom-color: $blueDarkCol;
          }
        }
      }
    }
    .customer-order {
      width: 40%;
      height: 96%;
      border: 2px solid $blueDarkCol;
      border-radius: 1%;
      margin-left: 0.5%;
      box-sizing: border-box;
      font-family: "Salsa", cursive;

      .order-main-info {
        width: 100%;
        height: 12%;

        .order-date {
          width: 100%;

          ul {
            width: 100%;
            list-style: none;

            margin-top: 3%;

            li {
              float: left;
              margin-left: 7%;
              font-weight: bolder;
              font-size: 12px;
              span {
                font-weight: normal;
                font-size: 11px;
              }
            }
          }
        }
        .restaurant-info {
          width: 100%;
          height: 60%;
          margin-top: 3%;
        }
      }
      .order-list {
        width: 100%;
        height: 88%;

        .table-order {
          width: 100%;
          margin-top: 4%;
          height: 80%;
          table {
            width: 100%;

            .main-row {
              height: 28px;
              background: $blueDarkCol;
              color: $greenYellCol;
              font-size: 15px;
            }
            .secandry-row {
              height: 20px;
              font-weight: normal;
              font-size: 13.5px;
              transition: 0.2s ease-in-out;
              cursor: pointer;
              &:hover {
                background: $greenYellCol;
                border: 1px solid $purpleCol;
              }
            }
            .row1 {
              width: 8%;
            }
            .row2 {
              width: 15%;
            }
            .row3 {
              width: 40%;
            }
          }
        }
        .total-bill {
          width: 100%;
          height: 10%;
          border-top: 1px solid $blueDarkCol;
          box-sizing: border-box;
          padding: 13px 7px 5px 10px;
          p {
            float: left;
            margin-left: 9%;
            margin-top: 5px;
            background: $greenYellCol;
          }
          button {
            width: 17%;
            height: 99%;
            margin-left: 25%;
            background: $blueDarkCol;
            border-bottom: 2px solid $purpleCol;
            border-left: 2px solid $purpleCol;
            font-size: 12px;
          }
        }
      }
    }
  }
  #table-number {
    width: 35px;
  }
}
</style>
