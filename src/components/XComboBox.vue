<template>
    <div class="combo-box" v-bind:class="{ active: isMenuVisible }">
        <x-dropdown class="combo-box-menu" v-model="isMenuVisible">
            <x-button v-for="(item, index) in items" v-bind:key="index" v-bind:class="{ active: item === value }" @click="selectItem(item);">
                <slot name="menuItem" v-bind:item="item">
                    {{ item }}
                </slot>
            </x-button>
        </x-dropdown>
        <div class="combo-box-border">
            <div class="combo-box-content">
                <slot v-bind:item="value" name="currentItem">
                    <x-text-box v-model="text" @blur="onInputBlur" @submit="onSubmit" @focusin="onFocusIn" ref="textBox">
                        
                    </x-text-box>
                </slot>
            </div>
            <x-button @mousedown="onMouseDown" @click="onClick">
                <x-dropdown-icon></x-dropdown-icon>
            </x-button>
        </div>
    </div>
</template>

<script lang="ts">
import { Component, Prop, Vue, Watch } from "vue-property-decorator";
import XButton from "./XButton.vue";
import XDropdown from "./XDropdown.vue";
import XDropdownIcon from "./XDropdownIcon.vue";
import XTextBox from "./XTextBox.vue";

@Component({
    components: {
        XButton,
        XDropdown,
        XDropdownIcon,
        XTextBox
    }
})
export default class XComboBox extends Vue {
    private text = "";
    @Prop() public value: any;
    @Prop() public items!: any[];
    @Prop() public validate?: (text: string) => (boolean);

    private isMenuVisible = false;

    mounted() {
        this.text = this.value;
    }

    onMouseDown(event: MouseEvent) {
        event.preventDefault();
        this.isMenuVisible = !this.isMenuVisible;
    }

    onClick(event: MouseEvent) {
        event.preventDefault();
        this.isMenuVisible = true;
    }

    onSubmit(text: string) {
        if (this.validate == null || this.validate(this.text)) {
            this.selectItem(this.text);
        }
        else {
            this.text = this.value;
        }
    }

    public selectItem(item: any) {
        this.$emit("input", item);
    }

    @Watch("value")
    onValueChanged(newValue: any, oldValue: any) {
        this.text = newValue;
    }

    onInputBlur() {
        this.onSubmit(this.text);
    }

    onFocusIn() {
        (this.$refs["textBox"] as XTextBox).selectAll();
    }
}

</script>

<style>
.combo-box {
    position: relative;
    box-sizing: border-box;
    flex-grow: 1;
}

.combo-box-border {
    display: flex;
    flex-direction: row;
    align-items: center;
    border: 1px solid var(--app-border-light);
    background-color: var(--app-overlay);
}

.combo-box-menu {
    display: flex;
    flex-direction: column;
    margin-bottom: 1px;
}

.combo-box:hover > .combo-box-border, .combo-box:focus-within > .combo-box-border {
    border: 1px solid var(--app-press-light);
}

.combo-box-content > .text-box {
}

.combo-box-border > button > .button-content {
    padding: 4px 2px !important;
}

.combo-box:hover > .combo-box-border > button, .combo-box.active > .combo-box-border > button, .combo-box:focus-within > .combo-box-border > button {
    background-color: var(--app-hover-light);
}

.combo-box-content input {
    font-family: inherit;
    width: 100%;
}

.combo-box-content {
    flex-grow: 1;
    flex-shrink: 1;
    padding: 2px 3px 2px 6px;
}
</style>