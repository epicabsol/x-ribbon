<template>
    <div class="dropdown-anchor">
        <div ref="dropdown" class="dropdown" v-bind:tabindex="value ? 0 : undefined" v-bind:class="{ visible: value }" v-on:blur="onBlur" @mousedown="eatMouseEvent" @mouseup="eatMouseEvent" @click="eatMouseEvent">
            <slot></slot>
        </div>
    </div>
</template>

<script lang="ts">
import { Component, Prop, Watch, Vue } from "vue-property-decorator";

@Component
export default class XDropdown extends Vue {
    @Prop() public value!: boolean;

    private setVisibility(visible: boolean) {
        this.$emit("input", visible);
    }

    @Watch("value")
    onPropertyChanged(value: boolean, oldValue: boolean) {
        if (value && !oldValue) {
            this.$nextTick(() => {
                const dropdown = this.$refs.dropdown as HTMLElement;
                dropdown.focus();
            });
        }
    }

    private onBlur() {
        this.setVisibility(false);
    }

    eatMouseEvent(event: MouseEvent) {
        event.stopPropagation();
    }
}
</script>

<style scoped>
.dropdown {
    z-index: 100;
    position: absolute;
    background-color: var(--app-overlay);
    top: 100%;
    min-width: 100%;
    text-align: left;
    box-sizing: border-box;
    display: flex;
    flex-direction: column;
    align-content: stretch;
    visibility: hidden;
    opacity: 0.0;
    transition: opacity 0.15s, transform 0.15s, visibility 0.0s linear 0.15s;
    transform: translateY(-5px);
    pointer-events: all;

    border: 1px solid var(--app-border-light);
    /*box-shadow: 0px 2px 15px rgba(0, 0, 0, 0.45);*/
}

.dropdown.visible {
    opacity: 1.0;
    visibility: visible;
    transform: none;
    transition: opacity 0.15s, transform 0.15s;
}

.dropdown:focus {
    outline: none;
}

.dropdown-anchor {
    position: absolute;
    left: 0px;
    right: 0px;
    top: 0px;
    bottom: 0px;
    align-self: stretch;
    display: flex;
    flex-direction: column;
    align-items: stretch;
    pointer-events: none;
}
</style>