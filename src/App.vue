<script setup lang="ts">
import FaceComponent from "./components/FaceComponent.vue";
import ButtonsComponentVue from "./components/ButtonsComponent.vue";

import { ref } from "vue";
import type { FaceType } from "./types";
import { IMAGES_MAPPING } from "./constants";
import html2canvas from "html2canvas";

type PART =
  | "accessories"
  | "ears"
  | "eyes"
  | "hair"
  | "mouth"
  | "neck"
  | "nose"
  | "leg"
  | "background";
const face = ref<FaceType>({
  accessories: "headphone",
  ears: "default",
  eyes: "default",
  hair: "default",
  mouth: "default",
  neck: "default",
  nose: "default",
  leg: "default",
  background: "blue70",
});
const changeTheme = ({ key, value }: { key: PART; value: string }) => {
  face.value[key] = value;
  //console.log(face.value[key], key);
};

const randomizeIt = () => {
  console.log(face.value);
  face.value = Object.keys(face.value).reduce((acc, att) => {
    // set attribute to random key
    if (!IMAGES_MAPPING[att]) {
      return acc; // don't change it if we don't have values : ex nose.
    }
    const collectionRandIndex = Math.floor(
      Math.random() * IMAGES_MAPPING[att].length
    );
    acc[att] = IMAGES_MAPPING[att][collectionRandIndex];
    return acc;
  }, face.value);
};

const downloadImage = async () => {
  const image: HTMLElement = document.querySelector(
    ".face-container"
  ) as HTMLElement;
  const printCanvas = await html2canvas(image);
  const link = document.createElement("a");
  link.setAttribute("download", "download.png");
  link.setAttribute(
    "href",
    printCanvas
      .toDataURL("image/png")
      .replace("image/png", "image/octet-stream")
  );
  link.click();
};
</script>

<template>
  <div class="container">
    <div class="alpaca-studio">
      <h2>ALPACA GENERATOR</h2>
      <div class="studio-container">
        <FaceComponent
          :face="face"
          :randomizeIt="randomizeIt"
          :downloadImage="downloadImage"
        />
        <ButtonsComponentVue :face="face" :changeTheme="changeTheme" />
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">
.container {
  background: #ddd;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
  flex-wrap: wrap;
  flex-direction: column;
  font-family: "Gill Sans", "Gill Sans MT", Calibri, "Trebuchet MS", sans-serif;
  font-weight: 900;
}
.alpaca-studio {
  display: flex;
  width: 50%;
  height: 50%;
  padding: 30px;
  flex-direction: column;
  gap: 15px;
  .studio-container {
    display: flex;
    flex-direction: row;
  }
}

@media (min-width: 1024px) {
}
</style>
