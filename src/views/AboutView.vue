<template>
  <div class="about">
    <div class="container" @mouseleave="handleMouseLeave">
      <div
          class="action up"
          v-if="scrollTop !== -1 * (totalHeight - pageHeight)"
          @mouseover="handleMouseOver('up')"
      ></div>
      <ul :style="{ transform: `translateY(${scrollTop}px)` }">
        <li
            v-for="(item, index) in imgs"
            :key="index"
            :style="{ padding: itemPadding + 'px' }"
        >
          <img
              :src="item"
              alt=""
              :style="{ width: iconSize[0] + 'px', height: iconSize[1] + 'px' }"
              @click="handleClick(index)"
          />
        </li>
      </ul>
      <div
          class="action dowm"
          v-if="scrollTop !== 0"
          @mouseover="handleMouseOver('down')"
      ></div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, computed } from "vue";

const props = defineProps({
  iconSize: {
    type: Array,
    default: () => [60, 60],
  },
  pageSize: {
    type: Number,
    default: 6,
  },
  itemPadding: {
    type: Number,
    default: 20,
  },
});
const list = [
  "logo.png",
  "back.svg",
  "behance.svg",
  "down.svg",
  "hands.svg",
  "hdd.svg",
  "next.svg", //
  "one.svg",
  "snow.svg",
  "three.svg",
  "up.svg",
  "upload.svg",
  "vip.svg", //
  "dvi.svg",
  "bone.svg",
  "bird.svg",
  "ipad.svg",
  "duck.svg",
  "deer.svg", //
  "fish.svg",
  "clap.svg",
  "eagle.svg",
];
const imgs = ref(
    list.map((item) => new URL(`../assets/${item}`, import.meta.url).href)
);

const scrollTop = ref(0);
const baseIndex = ref(0);

const actionHeight = computed(() => {
  return props.itemPadding+ "px";
});

const itemHeight = computed(() => {
  return props.iconSize[1] + 2 * props.itemPadding;
});
const containerBaseSize = computed(() => {
  return itemHeight.value + "px";
});
const containerHeight = computed(() => {
  return itemHeight.value * props.pageSize + "px";
});
const pageHeight = computed(() => {
  return props.pageSize * itemHeight.value;
});
const totalHeight = computed(() => {
  return imgs.value.length * itemHeight.value;
});

const handleMouseOver = async (direction: string) => {
  if (direction === "up") {
    if (
        scrollTop.value + (totalHeight.value - pageHeight.value) >
        pageHeight.value
    ) {
      scrollTop.value += -1 * pageHeight.value;
    } else {
      scrollTop.value = -1 * (totalHeight.value - pageHeight.value);
    }
  } else {
    if (scrollTop.value + pageHeight.value >= 0) {
      scrollTop.value = 0;
    } else {
      scrollTop.value += pageHeight.value;
    }
  }
};

const handleClick = (index: number) => {
  scrollTop.value = -1 * index * itemHeight.value;
  baseIndex.value = index;
};
const handleMouseLeave = () => {
  handleClick(baseIndex.value);
};
</script>

<style scoped lang="scss">
.container {
  overflow: hidden;
  transition: all 0.5s;
  position: relative;
  width: v-bind(containerBaseSize);
  height: v-bind(containerBaseSize);
  &:hover {
    height: v-bind(containerHeight);
  }
  .action {
    cursor: pointer;
    position: absolute;
    width: 100%;
    height: v-bind(actionHeight);
    z-index: 10;
    &.up {
      top: 0;
    }
    &.dowm {
      bottom: 0;
    }
  }
  ul {
    box-sizing: content-box;
    margin: 0;
    padding: 0;
    height: 100%;
    transition: all ease-in-out 1s;
    list-style: none;
    li {
      line-height: 0;
      position: relative;

      img {
        cursor: pointer;
        transition: all 0.5s;
        &:hover {
          scale: 1.3;
        }
      }
    }
  }
}
</style>

