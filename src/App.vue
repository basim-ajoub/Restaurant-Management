<template>
  <div id="app" class="app">
    <link rel="preconnect" href="https://fonts.googleapis.com" />
    <link rel="preconnect" href="https://fonts.gstatic.com"  />
    <link
      href="https://fonts.googleapis.com/css2?family=Josefin+Sans:ital,wght@1,200;1,300&family=Salsa&family=Bungee+Inline&family=Skranji&family=Luckiest+Guy&family=Puppies+Play&display=swap"
      rel="stylesheet"
    />

    <router-view />
  </div>
</template>

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
//for scroll bar Start
/* Works on Firefox */
* {
  scrollbar-width: 10px;
  scrollbar-color: $greenYellCol $blueDarkCol;
  scroll-behavior: auto;
}

/* Works on Chrome, Edge, and Safari */
*::-webkit-scrollbar {
  width: 15px;
   
}

*::-webkit-scrollbar-track {
  background: $blueDarkCol;
}

*::-webkit-scrollbar-thumb {
  background-color: $greenYellCol;
  border-radius: 20px;
  border: 3px solid $blueDarkCol;
}
//End Scroll bar
* {
  margin: 0;
  padding: 0;
}//All Right Reserved Basim Ajoub
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: $redCol;
   background-image: linear-gradient(40deg, $redCol, $whitCol);
  width: 100%;
  height: 643px;
  font-family: "Josefin Sans", Helvetica, Arial, sans-serif;
  
  stroke-miterlimit: 5;
}
//All Right Reserved Basim Ajoub
#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: $yellowCol;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
@media only screen and (min-height: 644px) {
  #app {
    height: 657px;
  }
}
</style>
