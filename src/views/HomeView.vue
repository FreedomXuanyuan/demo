<template>
  <div class="home">
    <div
        @touchstart="handleTouchStart"
        @touchmove="handleTouchMove"
        @touchend="handleTouchEnd"
        class="touch-area"
    >
      <!-- 这里是你的组件内容 -->
      <div class="boxlist">
        <div class="box">1</div>
        <div class="box">2</div>
        <div class="box">3</div>
        <div class="box">4</div>
        <div class="box">5</div>
        <div class="box">6</div>
        <div class="box">7</div>
        <div class="box">8</div>
        <div class="box">9</div>
        <div class="box">10</div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import {defineComponent} from 'vue';

export default defineComponent({
  setup() {
    let startX = 0;
    let startY = 0;

    const handleTouchStart = (event: TouchEvent) => {
      const touch = event.touches[0];
      startX = touch.pageX;
      startY = touch.pageY;
    };

    const handleTouchMove = (event: TouchEvent) => {
      const touch = event.touches[0];
      const deltaX = touch.pageX - startX;
      const deltaY = touch.pageY - startY;

      // 如果滑动方向是水平的，则执行相应操作
      if (Math.abs(deltaX) > Math.abs(deltaY)) {
        if (deltaX > 0) {
          // 向右滑动
        } else {
          // 向左滑动
        }
      } else if (Math.abs(deltaY) > Math.abs(deltaX)) {
        if (deltaY > 0) {
          // console.log('向下滑动')
        } else {
          // console.log('向上滑动')
        }
      }
    };
    const handleTouchEnd = (event: TouchEvent) => {
      const touch = event.changedTouches[0];
      const deltaX = touch.pageX - startX;
      const deltaY = touch.pageY - startY;
      var boxlistelement = document.getElementsByClassName('touch-area');
      var scrollTopSize = boxlistelement[0].children[0].children.length
      var scrollHeight = boxlistelement[0].children[0].scrollHeight
      var scrollIndex = Math.floor((boxlistelement[0].scrollTop + (scrollHeight/scrollTopSize)) / (scrollHeight/scrollTopSize))
      // 如果滑动方向是水平的，则执行相应操作
      if (Math.abs(deltaX) > Math.abs(deltaY)) {
        if (deltaX > 0) {
          // 向右滑动
        } else {
          // 向左滑动
        }
      } else if (Math.abs(deltaY) > Math.abs(deltaX)) {
        if (deltaY > 0) {
          // console.log('向下滑动' + deltaY)
          // let integerPartY = Math.floor(deltaY);
          // console.log(boxlistelement[0].scrollTop);
          console.log('1' + Math.ceil(boxlistelement[0].scrollTop / (scrollHeight/scrollTopSize)) * (scrollHeight/scrollTopSize))
          boxlistelement[0].scrollTop = Math.floor(boxlistelement[0].scrollTop / (scrollHeight/scrollTopSize)) * (scrollHeight/scrollTopSize)
          console.log('2' + Math.ceil(boxlistelement[0].scrollTop / (scrollHeight/scrollTopSize)) * (scrollHeight/scrollTopSize))
        } else {
          boxlistelement[0].scrollTop = Math.ceil(boxlistelement[0].scrollTop / (scrollHeight/scrollTopSize)) * (scrollHeight/scrollTopSize)
        }
      }
    };

    return {
      handleTouchStart,
      handleTouchMove,
      handleTouchEnd,
    };
  },
});
</script>
<style>
.touch-area {
  height: 90px;
  width: 60px;
  overflow: scroll;
  position: relative;
}
.boxlist {
  height: 360%;
  position: absolute;
  top: 0px;
}
.box {
  height: 10%;
  color: blue;
}
</style>