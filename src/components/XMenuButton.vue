<template>
    <x-button class="menu-button" :class="{ active: isMenuVisible }" :icon="icon" :name="name" @mousedown="onMouseDown" @click="onClick">
        <x-dropdown class="button-dropdown" v-model="isMenuVisible"><slot name="menu"></slot></x-dropdown>
        <div class="button-content">
            <slot>
                <i class="button-icon material-icons">{{ icon }}</i>
                <div class="button-label">
                    {{ name }}
                </div>
            </slot>
            <x-dropdown-icon></x-dropdown-icon>
        </div>
    </x-button>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
import XButton from "./XButton.vue";
import XDropdownIcon from "./XDropdownIcon.vue";
import XDropdown from "./XDropdown.vue";

@Component({
    components: {
        XButton,
        XDropdownIcon,
        XDropdown
    }
})
export default class XMenuButton extends Vue {
    private isMenuVisible = false;
    @Prop() public icon!: string;
    @Prop() public name!: string;

    onMouseDown(event: MouseEvent) {
        event.preventDefault();
        console.log("MenuButton Mouse Down!");
        this.isMenuVisible = !this.isMenuVisible;
    }

    onClick(event: MouseEvent) {

        event.preventDefault();
        console.log("MenuButton Mouse Down!");
        this.isMenuVisible = true;
    }
}
</script>

<style>
.menu-button {
    position: relative;
}

.button-dropdown .dropdown {
    min-width: 100%;
}

</style>