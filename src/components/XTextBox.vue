<template>
    <input class="text-box" type="text" v-model="text" @blur="onBlur" @keydown="onKeyDown" @focusin="onFocusIn" ref="input">
</template>

<script lang="ts">
import { Component, Prop, Vue, Watch } from "vue-property-decorator";

@Component
export default class XTextBox extends Vue {
    public text = "";
    @Prop() public value!: string;

    mounted() {
        this.text = this.value;
    }

    onInput(event: InputEvent) {
        this.$emit("input", this.value);
    }

    onBlur() {
        this.$emit("blur");
    }

    @Watch("text")
    onTextChanged(newText: string, oldText: string) {
        this.$emit("input", newText);
    }

    @Watch("value")
    onValueChanged(newValue: string, oldValue: string) {
        this.text = newValue;
    }

    onKeyDown(event: KeyboardEvent) {
        if (event.keyCode == 13) {
            this.$emit("submit", this.text);
            event.preventDefault();
        }
    }

    onFocusIn() {
        this.$emit("focusin");
    }

    public selectAll() {
        (this.$refs["input"] as HTMLInputElement).select();
    }
}
</script>

<style scoped>
.text-box {
    margin: 0px;
    border: none;
    background-color: var(--app-overlay);
}

.text-box:focus {
    outline: none;
}
</style>