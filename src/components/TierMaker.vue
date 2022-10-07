<template>
    <div id="tierMaker">
        <TierRow v-for="(tier,i) in tiers" :key="'tier-'+i" :tier="tiers[i]"/>
        <TierItems :items="[]"/>
    </div>
</template>
  
<script lang="ts" setup>
import Tier from "@/ts/Tier";
import { ref, onMounted } from "vue";
import TierRow from "./TierRow.vue";
import TierItems from "./TierItems.vue";

const tierCount = ref(5);
const tiers = ref<Tier[]>([]);
const items = ref<string[]>([]);

onMounted(() => {
    for (let i = 0; i < tierCount.value; i++) {
        tiers.value.push({
            name: "Tier " + (i + 1),
            color: i*30,
            items: []
        });
    }
});

</script>
  
<style lang="scss" scoped>
@import "@/scss/variables.scss";
#tierMaker {
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
    row-gap: 8px;
}
</style>

  