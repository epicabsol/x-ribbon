<template>
    <div id="app">
        <div class="header">
            XRibbon
            <x-ribbon v-bind:tabs="tabs">
                <template v-slot:content-home="{ }">
                    <div class="groups">
                        <x-ribbon-group name="Clipboard">
                            <x-button name="Paste" icon="content_paste"></x-button>
                            <x-ribbon-stack>
                                <x-button name="Cut" icon="content_cut"></x-button>
                                <x-button name="Copy" icon="content_copy"></x-button>
                                <x-button name="Format Painter" icon="format_paint"></x-button>
                            </x-ribbon-stack>
                        </x-ribbon-group>
                        <x-ribbon-group name="Font">
                            <x-ribbon-stack class="centered">
                                <x-ribbon-row>
                                    <x-button name="Increase Font Size" icon="format_size"></x-button>
                                    <x-button name="Decrease Font Size" icon="text_fields"></x-button>
                                    <x-separator></x-separator>
                                    <x-button name="Change Case" icon="title"></x-button>
                                    <x-separator></x-separator>
                                    <x-button name="Clear All Formatting" icon="format_clear"></x-button>
                                </x-ribbon-row>
                                <x-ribbon-row>
                                    <x-button name="Bold" icon="format_bold"></x-button>
                                    <x-button name="Italic" icon="format_italic"></x-button>
                                    <x-button name="Underline" icon="format_underline"></x-button>
                                    <x-button name="Strikethrough" icon="format_strikethrough"></x-button>
                                    <x-button name="Subscript" icon="subscript"></x-button>
                                    <x-button name="Superscript" icon="superscript"></x-button>
                                    <x-separator></x-separator>
                                    <x-button name="Text Effects and Typography" icon="brush"></x-button>
                                    <x-button name="Text Highlight Color" icon="font_download"></x-button>
                                    <x-button name="Font Color" icon="text_format"></x-button>
                                </x-ribbon-row>
                            </x-ribbon-stack>
                        </x-ribbon-group>
                        <x-ribbon-group name="Paragraph">
                            <x-ribbon-stack class="centered">
                                <x-ribbon-row>
                                    <x-button name="Bullets" icon="format_list_bulleted"></x-button>
                                    <x-button name="Numbering" icon="format_list_numbered"></x-button>
                                    <x-button name="Multilevel List" icon="read_more"></x-button>
                                    <x-separator></x-separator>
                                    <x-button name="Decrease Indent" icon="format_indent_decrease"></x-button>
                                    <x-button name="Increase Indent" icon="format_indent_increase"></x-button>
                                    <x-separator></x-separator>
                                    <x-button name="Sort" icon="sort_by_alpha"></x-button>
                                    <x-separator></x-separator>
                                    <x-button name="Show/Hide ¶" icon="format_textdirection_l_to_r"></x-button>
                                </x-ribbon-row>
                                <x-ribbon-row>
                                    <x-button name="Align Left" icon="format_align_left"></x-button>
                                    <x-button name="Center" icon="format_align_center"></x-button>
                                    <x-button name="Align Right" icon="format_align_right"></x-button>
                                    <x-button name="Justify" icon="format_align_justify"></x-button>
                                    <x-separator></x-separator>
                                    <x-button name="Line and Paragraph Spacing" icon="format_line_spacing"></x-button>
                                    <x-separator></x-separator>
                                    <x-button name="Shading" icon="palette"></x-button>
                                    <x-button name="Borders" icon="border_bottom"></x-button>
                                </x-ribbon-row>
                            </x-ribbon-stack>
                        </x-ribbon-group>
                        <x-ribbon-group name="Styles">
                        </x-ribbon-group>
                        <x-ribbon-group name="Editing">
                            <x-ribbon-stack>
                                <x-button name="Find" icon="search"></x-button>
                                <x-button name="Replace" icon="find_replace"></x-button>
                                <x-button name="Select" icon="mouse"></x-button>
                            </x-ribbon-stack>
                        </x-ribbon-group>
                        <x-ribbon-group name="Voice">
                            <x-button name="Dictate" icon="mic"></x-button>
                        </x-ribbon-group>
                        <x-ribbon-group name="Sensitivity">
                            <x-button name="Sensitivity" icon="description"></x-button>
                        </x-ribbon-group>
                        <x-ribbon-group name="Editor">
                            <x-button name="Editor" icon="edit"></x-button>
                        </x-ribbon-group>
                    </div>
                    
                </template>
                <template v-slot:content-insert="{ }">
                    Insert Content!
                </template>
            </x-ribbon>
        </div>
        <div class="content">
            <div class="page">

            </div>
        </div>
    </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import XRibbon from "./components/XRibbon.vue";
import XRibbonGroup from "./components/XRibbonGroup.vue";
import XRibbonStack from "./components/XRibbonStack.vue";
import XRibbonRow from "./components/XRibbonRow.vue";
import XButton from "./components/XButton.vue";
import XSeparator from "./components/XSeparator.vue";
import XRibbonTabInfo from "./models/XRibbonTabInfo";

@Component({
    components: {
        XRibbon,
        XRibbonGroup,
        XRibbonStack,
        XRibbonRow,
        XButton,
        XSeparator
    },
})
export default class App extends Vue {
    public tabs: XRibbonTabInfo[] = [
        new XRibbonTabInfo("home", "Home"),
        new XRibbonTabInfo("insert", "Insert"),
        new XRibbonTabInfo("design", "Design"),
        new XRibbonTabInfo("page-layout", "Page Layout"),
        new XRibbonTabInfo("references", "References"),
        new XRibbonTabInfo("mailings", "Mailings"),
        new XRibbonTabInfo("review", "Review"),
        new XRibbonTabInfo("view", "View"),
        new XRibbonTabInfo("developer", "Developer"),
        new XRibbonTabInfo("addins", "Add-ins")
    ];
}
</script>

<style>
body {
    margin: 0px;
    padding: 0px;
    box-sizing: border-box;
    display: inline-block;
    position: absolute;
    top: 0px;
    bottom: 0px;
    left: 0px;
    right: 0px;
    overflow: hidden;
}

.header {
    background-color: var(--app-accent);
    color: white;
}

.content {
    text-align: center;
    background-color: var(--app-content);
    overflow: auto;
}

.page {
    display: inline-block;
    width: 8.5in;
    height: 11in;
    background-color: white;
    outline: 1px solid var(--app-border-light);
    margin: 0.5in auto;
}

.groups {
    display: flex;
}

#app {
    --app-accent: rgb(40, 110, 190);
    --app-ribbon: rgb(240, 240, 240);
    --app-content: rgb(225, 225, 225);

    --app-border-light: rgba(0, 0, 0, 0.1);
    --app-hover-light: rgba(0, 0, 0, 0.08);
    --app-press-light: rgba(0, 0, 0, 0.15);

    --app-border-dark: rgba(255, 255, 255, 0.15);
    --app-hover-dark: rgba(255, 255, 255, 0.15);
    --app-press-dark: rgba(255, 255, 255, 0.3);

    font-family: Calibri, Arial, sans-serif;
    font-size: 12px;
    height: 100%;
    display: flex;
    flex-direction: column;
}
</style>
