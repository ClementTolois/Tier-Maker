<template>
    <div id="tierItems">
        <div id="tierItem" v-for="(item, i) in items" :key="'tierItem-' + i">
            {{ items[i] }}
        </div>
    </div>
</template>

<script lang="ts" setup>
import { onMounted, computed } from "vue";
import Tier from "@/ts/Tier";
import { Items } from "@/ts/Items";

const props = defineProps<{
    items: Items;
}>();
</script>

<style lang="scss" scoped>
@import "@/scss/variables.scss";
#tierItems {
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
    row-gap: 8px;
    background-color: white;
    border-radius: 4px;
    #tierItem {
        width: 100%;
        height: 100%;
        display: flex;
        flex-direction: row;
        column-gap: 8px;
    }
}
</style>
