<template>
    <button @mousedown="onMouseDown" @click="onClick" @mouseup="onMouseUp">
        <div class="button-content">
            <slot>
                <i class="button-icon material-icons">{{ icon }}</i>
                <div class="button-label">
                    {{ name }}
                </div>
            </slot>
        </div>
    </button>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class XButton extends Vue {
    @Prop() public icon!: string;
    @Prop() public name!: string;

    private onMouseDown(event: MouseEvent) {
        this.$emit("mousedown", event);
        //document.body.focus();
    }

    private onClick(event: MouseEvent) {
        this.$emit("click", event);
    }

    private onMouseUp(event: MouseEvent) {
        this.$emit("mouseup", event);
    }
}
</script>

<style>
button {
    background: none;
    border: none;
    outline: none;
    font-size: inherit;
    padding: 0px;
    display: flex;
    box-sizing: border-box;
}

button:hover, button.active {
    background-color: var(--app-hover-light);
}

button:active {
    background-color: var(--app-press-light);
}

.button-icon {
    font-size: 1.3em;
}

.button-label {
    text-align: center;
}

.button-content {
    padding: 4px;
}

/**
 * Dropdown buttons
 */
.dropdown button {
    /*height: 2em !important;*/
    align-items: center;
    white-space: pre;
}

.dropdown button .button-content {
    display: flex;
    flex-direction: row;
    align-items: center;
    padding: 6px 12px 6px 8px !important;
}

.dropdown button .button-label {
    display: unset !important;
}

.dropdown button .button-icon {
    width: 1em;
}

</style>