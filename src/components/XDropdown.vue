<template>
    <div class="dropdown-anchor">
        <div ref="dropdown" class="dropdown" tabindex="0" v-bind:class="{ visible: value }" v-on:blur="onBlur">
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
            console.log(this.value);
            this.$nextTick(() => {
                const dropdown = this.$refs.dropdown as HTMLElement;
                dropdown.focus();
            });
            console.log(this.$refs.dropdown);
            console.log(document.activeElement);
        }
    }

    private onBlur() {
        this.setVisibility(false);
    }
}
</script>

<style scoped>
.dropdown {
    z-index: 100;
    position: absolute;
    background-color: var(--app-overlay);
    top: 100%;
    text-align: left;
    box-sizing: border-box;
    display: flex;
    flex-direction: column;
    align-content: stretch;
    visibility: hidden;
    opacity: 0.0;
    transition: opacity 0.15s, transform 0.15s, visibility 0.0s linear 0.15s;
    transform: translateY(-5px);

    border: 1px solid var(--app-border-light);
    /*box-shadow: 0px 2px 15px rgba(0, 0, 0, 0.45);*/
}

.dropdown.visible {
    opacity: 1.0;
    visibility: visible;
    transform: none;
    transition: opacity 0.15s, transform 0.15s;
}

.dropdown.visible:focus {
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
}
</style>