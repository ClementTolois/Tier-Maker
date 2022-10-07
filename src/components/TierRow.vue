<template>
    <div id="tierRow">
        <span id="dragIndicator" class="material-icons">drag_indicator</span>
        <div @click="toggleEdit" id="tierName" :style="tierNameStyle">
            {{ tier.name }}
        </div>
        <TierItems :items="tier.items" />
        <div id="tierEditionWrapper" v-if="isEditing">
            <div id="tierEdition" @click.self="toggleEdit">
                <color-picker v-bind="color" @input="onInput" @animationend="onValidate"/>
            </div>
        </div>
    </div>
</template>

<script lang="ts" setup>
import { onMounted, computed, ref, reactive } from "vue";
import Tier from "@/ts/Tier";
import TierItems from "./TierItems.vue";
import ColorPicker from "@radial-color-picker/vue-color-picker";
import hsl from "hsl-to-hex";

const props = defineProps<{
    tier: Tier;
}>();

const isEditing = ref(false);

const color = reactive({
    hue: props.tier.color,
    saturation: 100,
    luminosity: 50,
    alpha: 1,
});

const tempColor = reactive({
    hue: props.tier.color,
    saturation: 100,
    luminosity: 50,
    alpha: 1,
});

const tierNameStyle = computed(() => {
    return `background-color: ${hsl(color.hue, color.saturation, color.luminosity)};`;
});

const toggleEdit = () => {
    isEditing.value = !isEditing.value;
};

const onInput = (hue: any) => {
    tempColor.hue = hue;
}

const onValidate = () => {
    setTimeout(() => {
        color.hue = tempColor.hue;
        toggleEdit();
    },650);
}
</script>

<style lang="scss" scoped>
@import "@/scss/index.scss";
@import "@radial-color-picker/vue-color-picker/dist/vue-color-picker.min.css";
#tierRow {
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: row;
    column-gap: 8px;
    #dragIndicator {
        display: flex;
        justify-content: center;
        align-items: center;
        box-sizing: border-box;
        color: white;
        cursor: pointer;
    }
    #tierName {
        height: 100%;
        display: flex;
        justify-content: center;
        align-items: center;
        text-overflow: ellipsis;
        white-space: nowrap;
        box-sizing: border-box;
        padding: 0 8px;
        user-select: none;
        border-radius: 4px;
        font-weight: 700;
        cursor: pointer;
    }
    #tierEditionWrapper {
        top: 0;
        left: 0;
        position: absolute;
        width: 100%;
        height: 100%;
        box-sizing: border-box;
        padding: 16px;
        backdrop-filter: brightness(.1);
        #tierEdition {
            width: 100%;
            height: 100%;
            display: flex;
            justify-content: center;
            align-items: center;
        }
    }
}
</style>
