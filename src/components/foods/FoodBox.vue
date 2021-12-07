<template>
  <div class="food-box-comp">
    <div id="food-box" class="food-box">
      <div class="icon-box">
        <i class="fas fa-utensils icon"></i>
      </div>
      <ul>
        <li>
          <p>Name :</p>
          <span id="show-food-name">{{ this.itemname }}</span>
        </li>
        <li>
          <p>Type :</p>
          <span id="show-food-type">{{ this.itemtype }}</span>
        </li>
        <li>
          <p>Price :</p>
          <span id="show-food-price">{{ this.itemprice }}</span>
        </li>
        <li class="btn-list"><button @click="EditBtn" id="menu-item-edit">Edit</button><button @click="DeleteBtn" id="menu-item-delete">Delete</button></li>
      </ul>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "FoodBoxComp",
  data(){
      return{
          edititemtype:"",
      };
  },
  props: ["itemname", "itemtype", "itemprice","key"],
  methods:{
   EditBtn(){
console.log("item you want to edit ", this.itemname ,this.itemtype,this.itemprice);
this.edititemtype = this.itemtype;
//to eupdate we use id of foof form component easely 
document.getElementById("menu-list").value = this.itemtype;
document.getElementById("food-price").value = this.itemprice;
document.getElementById("food-name").value = this.itemname;
document.getElementById("item-id").innerText = this.key;
console.log("item deleted succefully to be updated");
      },
   async   DeleteBtn(){
await axios.delete("http://localhost:3000/menu/" + this.key);
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
.food-box-comp {
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
        font-size: 14px;color: $purpleCol;
      }
    }
    ul {
      width: 100%;
      height: 58%;
      padding-top: 5%;
      list-style-type: none;
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
      }
    }
  }
}
</style>
