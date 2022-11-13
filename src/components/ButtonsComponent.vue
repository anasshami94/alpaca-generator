<script setup lang="ts">
import type { FaceType } from "@/types";
import { IMAGES_MAPPING } from "@/constants";
import { computed } from "@vue/reactivity";
import { ref } from "vue";
import type { ComputedRef } from "vue";
const props = withDefaults(
  defineProps<{ face: FaceType; changeTheme: Function}>(),
  {}
);
const keys: ComputedRef<string[]> = computed<string[]>(() =>
  Object.keys(IMAGES_MAPPING)
);
const selectedPart = ref<string>("ears");
const showThemes: ComputedRef<string[]> = computed<string[]>(
  () => (IMAGES_MAPPING as any)[selectedPart.value]
);
const selectedTheme: ComputedRef<string> = computed<string>(
  () => (props.face as any)[selectedPart.value]
);
</script>

<template>
  <div class="buttons-container">
    <h3>ACCESSORIZE THE ALPACA'S</h3>
    <div class="parts-container">
      <button
        v-for="buttonText in keys"
        v-bind:key="buttonText"
        :class="{ active: selectedPart === buttonText }"
        @click="() => (selectedPart = buttonText)"
      >
        {{ buttonText.toUpperCase() }}
      </button>
    </div>
    <h3>STYLES</h3>
    <div class="themes-container">
      <button
        v-for="buttonText in showThemes"
        v-bind:key="buttonText"
        :class="{ active: selectedTheme === buttonText }"
        @click="() => changeTheme({key: selectedPart, value: buttonText})"
      >
        {{ buttonText.toUpperCase() }}
      </button>
    </div>
  </div>
</template>

<style scoped lang="scss">
.buttons-container {
  padding-left: 15px;
  display: flex;
  flex-direction: column;
  gap: 15px;
  font-weight: 600;
  z-index: 1001;
  .parts-container,
  .themes-container {
    display: flex;
    gap: 5px;
    flex-wrap: wrap;
    padding: 8px 0px;
    button {
      border: 1px solid rgb(129, 129, 240);
      background: #ddd;
      padding: 8px 20px;
      border-radius: 25px;
      display: flex;
      cursor: pointer;
      &.active,
      &:hover {
        background: rgb(16, 16, 170);
        border: 1px solid rgb(16, 16, 170);
        color: white;
      }
    }
  }
}
</style>
