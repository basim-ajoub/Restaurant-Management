<template>
  <div class="admin-f-comp">
    <div class="comp-title">
      <h1>Foods</h1>
    </div>
    <div class="food-container">
      <div class="food-form-comp">
        <FoodsFormComp />
      </div>

      <div class="menu-box">
        <div class="filter-btn">
          <select v-model="filtertype" name="menu-list" id="filter-type">
            <option value="all" selected>All</option>
            <option value="food">Food</option>
            <option value="sweet">Sweet</option>
            <option value="drink">Drink</option>
          </select>
          <button @click="FilterBtn">Filter</button>
        </div>

        <div class="show-all-food-added">
          <div
            v-for="item in menuitems"
            :key="item.key"
            id="food-box-added"
            class="food-box-added"
          >
            <FoodBoxComp
              :itemname="item.name"
              :itemtype="item.type"
              :itemprice="item.price"
              :key="item.key"
            />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";
import FoodsFormComp from "../foods/FoodForm.vue";
import FoodBoxComp from "../foods/FoodBox.vue";
export default {
  name: "AdminFoodComp",
  props: ["edititemtype"],
  data() {
    return {
      showbills: {},
      menuitems: {},
      testdata: this.edititemtype,
    };
  },

  mounted() {
    this.showMenuItems();
  },
  components: {
    FoodBoxComp,
    FoodsFormComp,
  },
  methods: {
    showtest() {
      console.log("200", this.itemname);
    },
    async showMenuItems() {
      let itemMenu = await axios.get("http://localhost:3000/menu");
      console.log(itemMenu.data, "menu items");
      this.menuitems = itemMenu.data;
    },
    async FilterBtn() {
      let filterBtn = this.filtertype;
      if (filterBtn == "sweet") {
        let itemMenu = await axios.get(
          "http://localhost:3000/menu?type=" + filterBtn
        );
        console.log(itemMenu.data, "sweet  items filter");
        this.menuitems = itemMenu.data;
      } else if (filterBtn == "food") {
        let itemMenu = await axios.get(
          "http://localhost:3000/menu?type=" + filterBtn
        );
        console.log(itemMenu.data, "food  items filter");
        this.menuitems = itemMenu.data;
      } else if (filterBtn == "drink") {
        let itemMenu = await axios.get(
          "http://localhost:3000/menu?type=" + filterBtn
        );
        console.log(itemMenu.data, "drink  items filter");
        this.menuitems = itemMenu.data;
      } else {
        let itemMenu = await axios.get("http://localhost:3000/menu");
        console.log(itemMenu.data, "All  items filter");
        this.menuitems = itemMenu.data;
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
.admin-f-comp {
  width: 99%;
  height: 98%;
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
  .food-container {
    width: 100%;
    height: 79%;
  }
  .food-form-comp {
    width: 50%;
    height: 90%;
    padding-top: 8%;
    padding-left: 5%;
    box-sizing: border-box;
    position: relative;
    float: left;
  }
  .menu-box {
    width: 50%;
    height: 100%;

    margin-left: 49%;
    box-sizing: border-box;
    position: relative;

    .filter-btn {
      width: 100%;
      height: 10%;
      box-sizing: border-box;

      padding-top: 2%;
      select {
        width: 40%;
        height: 60%;
        background: $blueDarkCol;
        color: $greenYellCol;
        border: 1px;
      }
      button {
        width: 15%;
        height: 70%;
        margin-left: 2%;
        background: $blueDarkCol;
        color: $greenYellCol;
        border-bottom: 2px solid $purpleCol;
        border-left: 2px solid $purpleCol;
        font-size: 12px;
        cursor: pointer;
      }
    }

    .show-all-food-added {
      width: 98%;
      background: $blueDarkCol;
      border-radius: 2%;
      height: 89%;

      overflow: hidden;
      overflow-y: scroll;
      box-sizing: border-box;
      position: relative;

      .food-box-added {
        width: 23%;
        height: 25%;

        margin-left: 7%;
        margin-bottom: 5%;
        float: left;
      }
    }
  }
}
</style>
