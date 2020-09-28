<template>
    <div class="combo-box">
        <x-dropdown class="combo-box-menu" v-model="isMenuVisible">
            <x-button v-for="(item,index) in items" v-bind:key="index" @click="selectItem(item);">
                <slot name="menuItem" v-bind:item="item">
                    {{ item }}
                </slot>
            </x-button>
        </x-dropdown>
        <div class="combo-box-border">
            <div class="combo-box-content">
                <slot v-bind:item="value" name="currentItem">
                    {{ value }}
                </slot>
            </div>
            <x-button @mousedown="onMouseDown" @click="onClick">
                <x-dropdown-icon></x-dropdown-icon>
            </x-button>
        </div>
    </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
import XButton from "./XButton.vue";
import XDropdown from "./XDropdown.vue";
import XDropdownIcon from "./XDropdownIcon.vue";

@Component({
    components: {
        XButton,
        XDropdown,
        XDropdownIcon
    }
})
export default class XComboBox extends Vue {
    @Prop() public value: any;
    @Prop() public items!: any[];

    private isMenuVisible = false;

    onMouseDown(event: MouseEvent) {
        event.preventDefault();
        this.isMenuVisible = !this.isMenuVisible;
    }

    onClick(event: MouseEvent) {
        event.preventDefault();
        this.isMenuVisible = true;
    }

    public selectItem(item: any) {
        this.$emit("input", item);
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

.combo-box:hover > .combo-box-border {
    border: 1px solid var(--app-press-light);
}

.combo-box-content {
    margin: 3px 3px 3px 6px;
}

.combo-box-border > button > .button-content {
    padding: 4px 2px !important;
}

.combo-box:hover > .combo-box-border > button {
    background-color: var(--app-hover-light);
}
</style>