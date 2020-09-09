<template>
    <div class="separator">
    </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

@Component
export default class XSeparator extends Vue {

}
</script>

<style scoped>
.separator {
    display: inline-block;
    width: 1px;
    margin: 0px 4px;
    background-color: var(--app-border-light);
}
</style>