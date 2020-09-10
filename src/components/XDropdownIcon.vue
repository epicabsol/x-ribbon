<template>
    <svg class="dropdown-icon" width="8" height="4">
        <polygon points="0,0 8,0 4,4" />
    </svg>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

@Component
export default class XDropdownIcon extends Vue {
}
</script>

<style scoped>
.dropdown-icon {
    padding: 2px 0px;
    margin: 4px;
}
</style>