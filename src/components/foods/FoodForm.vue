<template>
  <div class="admin-food-comp">
    <div class="form-box">
      <ul>
        <li>
          <p>Name :</p>
          <input
            id="food-name"
            v-model="foodname"
            placeholder="Food Name"
            type="text"
          />
        </li>
        <li>
          <p>Price :</p>
          <input
            id="food-price"
            v-model="foodprice"
            placeholder="Food Price"
            type="number"
          />
        </li>
        <li>
          <p>Type :</p>
          <select v-model="foodtype" name="menu-list" id="menu-list">
            <option value="" selected disabled hidden>Choose here</option>
            <option value="food" selected>Food</option>
            <option value="sweet">Sweet</option>
            <option value="drink">Drink</option>
          </select>
          <p id="item-id-field">Item Id : <span id="item-id"></span></p>
        </li>
        <li>
          <button class="add-food" id="add-food" @click="AddFood">Add</button>
        </li>
        <li id="warn-note" class="warn-note">
          <p>Please Fill Out All Fields</p>
        </li>
      </ul>
    </div>
  </div>
</template>
<script>
import axios from "axios";

export default {
  name: "FoodFormComp",

  data() {
    return {
      foodname: "",
      foodprice: "",
      foodtype: "",
    };
  },
  mounted() {
    this.ShowAllMenu();
  },
  methods: {
    async AddFood() {
      let x = document.getElementById("food-name").value;
      let y = document.getElementById("food-price").value;
      let z = document.getElementById("menu-list").value;
      let OldId = Number(document.getElementById("item-id").innerText);
      console.log(OldId, "oldid");
      if (this.foodname && this.foodtype && this.foodprice != null) {
        if (OldId == 0) {
          let food = await axios.post("http://localhost:3000/menu", {
            name: this.foodname,
            type: this.foodtype,
            price: this.foodprice,
            id: this.id,
          });
          console.log("food added completely", food.status);
        } else {
          console.log("Please Fill Out All Fields", x, y, z);
          let food = await axios.put("http://localhost:3000/menu/" + OldId, {
            name: this.foodname,
            type: this.foodtype,
            price: this.foodprice,
            id: OldId,
          });
          console.log("item Updated Succefully ", food);
        }
      } else {
        document.getElementById("warn-note").style.display = "block";
        console.log("Error Field cant be Empty");
      }
      location.reload();
    },
    async ShowAllMenu() {
      let menu = await axios.get("http://localhost:3000/menu");
      console.log("menu", menu);
      if (menu.data[0] != null) {
        document.getElementById("show-food-name").innerText = menu.data[0].name;
        document.getElementById("show-food-price").innerText =
          menu.data[0].price + " $";
        document.getElementById("show-food-type").innerText = menu.data[0].type;
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
.admin-food-comp {
  width: 99%;
  height: 98%;

  .form-box {
    width: 60%;
    height: 50%;
    ul {
      list-style-type: none;
      width: 100%;
      height: 100%;

      li {
        width: 100%;
        height: 15%;
        color: $blueDarkCol;
        margin-bottom: 5%;
        p {
          width: 35%;
          float: left;
          font-weight: bold;
          text-align: left;
          margin-left: 2%;
        }
        input {
          width: 50%;
          height: 60%;
          border: 1px;
          border-radius: 5%;
          padding: 3px 3px 3px 3px;
          background: $blueDarkCol;
          color: $greenYellCol;
          font-size: 13px;
          letter-spacing: 0.5px;
        }
        select {
          width: 52%;
          height: 80%;
          background: #111324;
          color: $greenYellCol;
        }
        #item-id-field {
          display: none;
        }
        button {
          width: 25%;
          height: 99%;
          margin-left: 32%;
          background: #111324;
          border-bottom: 2px solid #7856ff;
          border-left: 2px solid #7856ff;
          font-size: 12px;
          color: $greenYellCol;
          cursor: pointer;
        }
      }
      .warn-note {
        width: 100%;

        color: red;
        display: none;
        p {
          width: 100%;
        }
      }
    }
  }
}
</style>
