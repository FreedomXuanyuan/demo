<template>
<!--  <nav>-->
<!--    <router-link to="/">Home</router-link> |-->
<!--    <router-link to="/about">About</router-link>-->
<!--  </nav>-->
<!--  <router-view/>-->
<!--  <div ref="threeContainer"></div>-->
<!--  <ThreeView />-->
  <div>{{ state.demo }}</div>
  <div class="title" v-for="(item, index) in state.demoTitle" @click="chaneColor(item)" :class="{active : item.title === state.changeColorNum}">{{ item.title }}</div>
  <hr>
  <div>This is a demo</div>
</template>
<script setup lang="ts">
import * as THREE from 'three';
import ThreeView from './views/ThreeView.vue'
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
  ],
  changeColorNum: "Demo1",
})
const chaneColor = (item: any) => { //更改颜色
  state.changeColorNum = item.title;
  console.log(item, state.changeColorNum);
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
.title {
  &.active {
    background: #cdf;
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
