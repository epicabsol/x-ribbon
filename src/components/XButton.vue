<template>
    <button>
        <i class="button-icon material-icons">{{ icon }}</i>
        <div class="button-label">
            {{ name }}
        </div>
    </button>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class XButton extends Vue {
    @Prop() public icon!: string;
    @Prop() public name!: string;
}
</script>

<style scoped>
button {
    background: none;
    border: none;
    outline: none;
    padding: 4px;
    font-size: inherit;
}

button:hover {
    background-color: var(--app-hover-light);
}

button:active {
    background-color: var(--app-press-light);
}

.button-label {
    text-align: center;
}

</style>