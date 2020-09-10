<template>
    <div class="ribbon-group">
        <div class="ribbon-group-content">
            <slot></slot>
        </div>
        <div class="ribbon-group-caption">
            {{ name }}
        </div>
    </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class XRibbonGroup extends Vue {
    @Prop() public name!: string;
}
</script>

<style>
.ribbon-group {
    display: flex;
    flex-direction: column;
    border-right: 1px solid var(--app-border-light);
    margin: 6px 0px 4px 6px;
    padding: 0px 6px 0px 0px;
}

.ribbon-group-content {
    flex-grow: 1;
    flex-shrink: 1;
    display: flex;
    flex-direction: row;
}

.ribbon-group-caption {
    opacity: 0.6;
    font-size: 0.95em;
    text-align: center;
    flex-grow: 0;
    margin-bottom: -3px;
    padding-top: 5px;
}

.ribbon-group .button-content {
    display: flex;
    flex-direction: column;
    align-items: center;
}

.ribbon-group button .button-icon {
    display: inline-block;
    font-size: 3em;
    width: 1em;
}

.ribbon-group .ribbon-stack .separator {
    height: 100%;
}

.ribbon-group .ribbon-stack button {
    height: 2em;
    align-items: center;
}

.ribbon-group .ribbon-stack .button-content {
    display: flex;
    flex-direction: row;
    align-items: center;
    padding: 2px 6px 2px 4px;
    width: unset;
}

.ribbon-group .ribbon-stack button .button-icon {
    font-size: 1.3em;
    margin-right: 3px;
}

.ribbon-group .ribbon-stack .ribbon-row button {
    height: auto;
}

.ribbon-group .ribbon-stack .ribbon-row button .button-content {
    padding: 4px;
}

.ribbon-group .ribbon-stack .ribbon-row button .button-icon {
    width: 1em;
    height: 1em;
    margin-right: 0px;
}

.ribbon-group .ribbon-stack button .button-dropdown-icon {
    margin-left: 2px;
}

.ribbon-group .ribbon-stack .ribbon-row button .button-label {
    display: none;
}
</style>