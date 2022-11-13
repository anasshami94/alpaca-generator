<script setup lang="ts">
import type { FaceType } from "../types";

withDefaults(
  defineProps<{
    face: FaceType;
    randomizeIt: Function;
    downloadImage: Function;
  }>(),
  {}
);
</script>

<template>
  <div class="alpaca-container">
    <div
      class="face-container"
      :style="{
        background: `url(src/assets/images/backgrounds/${face.background}.png)`,
      }"
    >
      <div class="accessory">
        <img :src="`src/assets/images/accessories/${face.accessories}.png`" />
      </div>
      <div class="ears">
        <img :src="`src/assets/images/ears/${face.ears}.png`" />
      </div>
      <div class="eyes">
        <img :src="`src/assets/images/eyes/${face.eyes}.png`" />
      </div>
      <div class="hair">
        <img :src="`src/assets/images/hair/${face.hair}.png`" />
      </div>
      <div class="mouth">
        <img :src="`src/assets/images/mouth/${face.mouth}.png`" />
      </div>
      <div class="neck">
        <img :src="`src/assets/images/neck/${face.neck}.png`" />
      </div>
      <div class="leg">
        <img :src="`src/assets/images/leg/${face.leg}.png`" />
      </div>
      <div class="nose">
        <img :src="`src/assets/images/nose.png`" />
      </div>
    </div>
    <div class="btns-container">
      <button @click="() => randomizeIt()">Random</button>
      <button @click="downloadImage()">Download</button>
    </div>
  </div>
</template>

<style scoped lang="scss">
.alpaca-container {
  display: flex;
  flex-direction: column;
}
.face-container {
  width: 350px;
  height: 345px;
  position: relative;
  * {
    scale: 0.7;
  }
  .neck,
  .accessory,
  .ears,
  .eyes,
  .mouth,
  .nose,
  .hair {
    position: absolute;
    left: -50%;
    top: -55%;
  }
  .neck {
    z-index: 1;
  }
  .ears {
    z-index: 2;
  }
  .accessory {
    z-index: 10;
  }
  .nose {
    z-index: 5;
  }
  .mouth {
    z-index: 6;
  }
  .hair {
    z-index: 8;
  }
  .eyes {
    z-index: 9;
  }
  .leg {
    position: absolute;
    left: -50%;
    bottom: -55%;
  }
}
.btns-container {
  display: flex;
  gap: 15px;
  align-items: center;
  justify-content: center;
  margin-top: 15px;
  button {
    padding: 8px 20px;
    background: #fff;
    border: 0;
    cursor: pointer;
    z-index: 1001;
  }
}
</style>
