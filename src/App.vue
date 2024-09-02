<template>
<!--  <nav>-->
<!--    <router-link to="/">Home</router-link> |-->
<!--    <router-link to="/about">About</router-link>-->
<!--  </nav>-->
<!--  <router-view/>-->
<!--  <div ref="threeContainer"></div>-->
<!--  <ThreeView />-->
  <div>{{ state.demo }}</div>
  <div class="ceshi">
    <div class="title" style="user-select: none" v-for="(item, index) in state.demoTitle" @click="chaneColor(item)" :class="{active : item.title === state.changeColorNum}">{{ item.title }}</div>
  </div>
  <hr>
  <div>
    <div @click="changeTrue" style="cursor: pointer;">
      change
    </div>
    {{state.demoTrue ? "yes": "no"}}<br>
    123<br>
    {{formatGetDate()}}
  </div>
  <div class="switchBox">
    <div class="switch" @click="changeSwitchTrue" :class="{active : state.switchTrue==true}">

    </div>
  </div>
  <div  v-html="state.demoHtml"></div>
</template>
<script setup lang="ts">
import {reactive} from "vue";

const state = reactive<any>({
  chartsStatus: '',
  dec: {} as any,
  demo: 100,
  demoTitle: [
    {title: 'Demo1'},
    {title: 'Demo2'},
    {title: 'Demo3'},
    {title: 'Demo4'},
    {title: 'Demo5'},
  ],
  changeColorNum: "Demo1",
  demoHtml: '<h1 id="demoHtml">This is a Test!</h1>',
  demoTrue: false,
  switchTrue: true,
})
const changeTrue = () => {
  state.demoTrue = state.demoTrue != true;
}
const changeSwitchTrue = () => {
  state.switchTrue = state.switchTrue != true;
}
const chaneColor = (item: any) => { //更改颜色
  state.changeColorNum = item.title;
}
const formatGetDate = () => {
  return new Date();
}
</script>
<!--<script setup lang="ts">-->
<!--</script>-->

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.ceshi {
  display: flex;
  .title {
    &.active {
      background: #cdf;
    }
    display: flex;
    width: 20%;
    cursor: pointer;
  }
}
.switchBox {
  width: 70px;
  height: 30px;
  position: relative;
  border: 6px solid #ccc;
  border-radius: 200px;
  .switch {
    width: 30px;
    height: 30px;
    box-sizing: border-box;
    border: 6px solid #000;
    border-radius: 50%;
    position: absolute;
    background: #000;
    cursor: pointer;
    //left: 0;
    right: 0;
    transition: .3s;
    &.active {
      //position: absolute;
      right: 40px;
      background: rgba(0, 0, 0, 0);
    }
  }
}
nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
