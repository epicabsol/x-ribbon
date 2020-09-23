<template>
    <div class="split-button">
        <x-button class="split-button-main">
            <slot>
                <i class="button-icon material-icons">{{ icon }}</i>
            </slot>
        </x-button>
        <x-menu-button class="split-button-menu" icon="">
            <template>
                <div class="button-label">
                    {{ name }}
                </div>
            </template>
            <template v-slot:menu>
                <slot name="menu"></slot>
            </template>
        </x-menu-button>
    </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
import XButton from "./XButton.vue";
import XMenuButton from "./XMenuButton.vue";

@Component({
    components: {
        XButton,
        XMenuButton
    }
})
export default class XSplitButton extends Vue {
    @Prop() public icon!: string;
    @Prop() public name!: string;
}
</script>

<style>
.split-button {
    display: flex;
    align-items: stretch;
}

.split-button > .split-button-menu {
    
}

.ribbon-group-content > .split-button {
    flex-direction: column;
}

.ribbon-group-content > .split-button > .split-button-main {
    flex-grow: 1;
}

.ribbon-group-content > .split-button > .split-button-main > .button-content .button-icon {
    font-size: 3em;
}

.ribbon-group-content > .split-button > .split-button-menu {
    display: flex;
    flex-direction: column;
    align-items: center;
}

/* Huh? Why the heck did I write this?
.ribbon-group-content > .split-button > .split-button-menu > .button-content .button-icon {
    display: none;
}*/
</style>