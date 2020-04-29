<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
body{
  background-color: #f5f5f5;
  padding: 0;
  margin: 0;
}
.wrapper{
  width: 650px;
  background-color: white;
  margin: 0 auto;
  height: 100vh;
}
.navbar{
  padding: 20px;
}
.brand{
  width: 150px;
  margin: 0 auto;
  img{
    width: 100%;
  }
}
.search{
  width: 350px;
  height: 35px;
  background-color: #e5e9ec;
  float: right;
  border-radius: 2px;
  padding: 5px;
  border-radius: 25px;
  i{
    margin-right: 10px;
    color: silver
  }
  input{
    width: calc(100% - 40px);
    height: calc(100% - 1px);
    background-color: #e5e9ec;
    border: none;
    outline: none ;
    padding: 10px;
    box-sizing: border-box;
    &:focus{
      background-color: white
    }
  }

}
</style>
