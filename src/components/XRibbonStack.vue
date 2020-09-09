<template>
    <div class="ribbon-stack">
        <slot></slot>
    </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

@Component
export default class XRibbonStack extends Vue {

}
</script>

<style scoped>
.ribbon-stack {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
}

.ribbon-stack.centered {
    justify-content: space-evenly;
}
</style>