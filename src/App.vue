<template>
  <div id="app"> 
    <hello></hello>
  </div>
</template>

<script>
import Hello from './components/Hello'

export default {
  name: 'app',
  components: {
    Hello
  }
}
</script>

<style>

* {
    margin: 0; padding: 0;
    box-sizing: border-box;
    font-family: Source Sans Pro, sans-serif, arial;
}

html {
    background-color: #eeeeee;
    width: 100%; height: 100%;
}

.topbar {
    position: fixed;
    width: 100%; height: 50px;
    background-color: #678;
    border-bottom: 1px solid black;
}

    .topbar h1 {
        margin: 8px 0 0 10px;
        color: #eeeeee;
    }

.menugauche {
    position: fixed;
    float: left;
    margin-top: 50px;
    width: 20%; height: calc(100% - 50px);
    border-right: 1px solid black;
    padding-left: 40px;
    overflow-y: scroll;
    background-color: #ffffff;
}

    .menugauche > ul > li {
        font-size: 20px;
        color: #999999;
        line-height: 40px;
    }

.corps {
    position: fixed;
    background-color: #bcd;
    top: 90px;
    right: 40px;
    width: calc(80% - 80px); height: calc(100% - 150px);
    border: 1px solid black;
    padding: 10px;
    overflow-y: scroll;
}

.incorps {
  width: 100%; height: 100%;
  position: relative;
}

  .corps .btnbtot1 {
      background-color: #73a8ee;
      margin: 10px auto;
      text-align: center;
      cursor: pointer;
      color: blue;
      font-size: 14px;
      padding: 7px;
  }

.btnbtot2 {
    display: none;
    position: absolute;
    bottom: 10px; right: 40px;
    background-color: #73df8b;
    text-align: center;
    cursor: pointer;
    color: blue;
    font-size: 14px;
    padding: 7px 18px;
}
</style>
