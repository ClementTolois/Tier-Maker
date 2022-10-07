<template>
  <div id="homeView">
    <TierMaker/>
  </div>
</template>

<script lang="ts" setup>
import TierMaker from "@/components/TierMaker.vue";
</script>

<style lang="scss" scoped>
@import "@/scss/variables.scss";
#homeView {
    width: 100%;
    height: 100%;
    background-color: $black;
    box-sizing: border-box;
    padding: 16px;
}
</style>
