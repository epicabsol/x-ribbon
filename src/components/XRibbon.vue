<template>
    <div>
        <div v-for="(tab, index) in tabs" v-bind:key="tab.id" class="tab-header" v-bind:class="{ 'active': currentTab == index }" v-on:mousedown="tabClicked(index)">
            {{ tab.text }}
        </div>
        <div class="tab-content">
            <keep-alive>
                <slot v-bind:name="'content-' + tabs[currentTab].id"></slot>
            </keep-alive>
        </div>
    </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
import XRibbonTabInfo from "../models/XRibbonTabInfo";

@Component
export default class XRibbon extends Vue {
    @Prop() public tabs!: XRibbonTabInfo[];
    private currentTab = 0;

    private tabClicked(index: number) {
        this.currentTab = index;
    }
}
</script>

<style scoped>
.tab-header {
    display: inline-block;
    padding: 8px 15px;
    cursor: default;
    user-select: none;
    font-size: 1.1em;
}

.tab-header:hover {
    background-color: var(--app-hover-dark);
}

.tab-header.active {
    color: var(--app-accent);
    background-color: var(--app-ribbon);
}

.tab-content {
    color: black;
    background-color: var(--app-ribbon);
    border-bottom: 1px solid var(--app-border-light);
    height: 8em;
    display: flex;
    flex-direction: row;
    font-size: 1.1em;
}
</style>