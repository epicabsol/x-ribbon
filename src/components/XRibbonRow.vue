<template>
    <div class="ribbon-row">
        <slot></slot>
    </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

@Component
export default class XRibbonRow extends Vue {

}
</script>

<style scoped>
.ribbon-row {
    display: flex;
    flex-direction: row;
    align-items: flex-start;
}
</style>