<template>
    <div id="app">
        <div class="header">
            XRibbon
            <x-ribbon v-bind:tabs="tabs">
                <template v-slot:content-home="{ }">
                    <div class="groups">
                        <x-ribbon-group name="Clipboard">
                            <x-split-button name="Paste" icon="content_paste">
                                <template v-slot:menu>
                                    <x-button name="Keep Source Formatting" icon=""></x-button>
                                    <x-button name="Match Formatting" icon=""></x-button>
                                    <x-button name="Keep Text Only" icon=""></x-button>
                                    <x-separator></x-separator>
                                    <x-button name="Paste Special..." icon=""></x-button>
                                </template>
                            </x-split-button>
                            <x-ribbon-stack>
                                <x-button name="Cut" icon="content_cut"></x-button>
                                <x-button name="Copy" icon="content_copy"></x-button>
                                <x-button name="Format Painter" icon="format_paint"></x-button>
                            </x-ribbon-stack>
                        </x-ribbon-group>
                        <x-ribbon-group name="Font">
                            <x-ribbon-stack class="centered">
                                <x-ribbon-row>
                                    <x-combo-box style="width: 8em;" v-bind:items="fonts" v-model="currentFont" v-bind:style="{ 'font-family': currentFont }">
                                        <template v-slot:menuItem="{ item }">
                                            <span v-bind:style="{ 'font-family': item }">{{ item }}</span>
                                        </template>
                                        <!--<template v-slot:currentItem="{ item }">
                                            <span>{{ item }}</span>
                                        </template>-->
                                    </x-combo-box>
                                    <x-combo-box class="shift-left" style="width: 4em;" v-bind:items="fontSizes" v-model="currentFontSize" :validate="onValidateFontSize">
                                        <template v-slot:menuItem="{ item }">
                                            <span v-bind:style="{ 'font-size': item + 'pt' }">{{ item }}</span>
                                        </template>
                                    </x-combo-box>
                                    <x-button name="Increase Font Size" icon="format_size"></x-button>
                                    <x-button name="Decrease Font Size" icon="text_fields"></x-button>
                                    <x-separator></x-separator>
                                    <x-menu-button name="Change Case" icon="title">
                                        <template v-slot:menu>
                                            <x-button name="Sentence case." icon="title"></x-button>
                                            <x-button name="lowercase" icon=""></x-button>
                                            <x-button name="UPPERCASE" icon=""></x-button>
                                            <x-button name="Capitalize Each Word" icon=""></x-button>
                                            <x-button name="tOGGLE cASE" icon=""></x-button>
                                        </template>
                                    </x-menu-button>
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
                                    <x-menu-button name="Text Effects and Typography" icon="brush">
                                        <template v-slot:menu>
                                            <x-button name="Outline" icon=""></x-button>
                                            <x-button name="Shadow" icon=""></x-button>
                                            <x-button name="Reflection" icon=""></x-button>
                                            <x-button name="Glow" icon=""></x-button>
                                            <x-button name="Number Styles" icon=""></x-button>
                                            <x-button name="Ligatures" icon=""></x-button>
                                            <x-button name="Stylistic Sets" icon=""></x-button>
                                        </template>
                                    </x-menu-button>
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
                                    <x-menu-button name="Multilevel List" icon="read_more">
                                        <template v-slot:menu>
                                            <x-button name="Change List Level" icon=""></x-button>
                                            <x-button name="Define New Multilevel List..." icon=""></x-button>
                                            <x-button name="Define New List Style..." icon=""></x-button>
                                        </template>
                                    </x-menu-button>
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
                                    <x-menu-button name="Line and Paragraph Spacing" icon="format_line_spacing">
                                        <template v-slot:menu>
                                            <x-button name="1.0" icon=""></x-button>
                                            <x-button name="1.15" icon=""></x-button>
                                            <x-button name="1.5" icon=""></x-button>
                                            <x-button name="2.0" icon=""></x-button>
                                            <x-button name="2.5" icon=""></x-button>
                                            <x-button name="3.0" icon=""></x-button>
                                            <x-button name="Line Spacing Options..." icon=""></x-button>
                                            <x-separator></x-separator>
                                            <x-button name="Add Space Before Paragraph" icon=""></x-button>
                                            <x-button name="Remove Space After Paragraph" icon=""></x-button>
                                        </template>
                                    </x-menu-button>
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
                                <x-menu-button name="Select" icon="mouse">
                                    <template v-slot:menu>
                                        <x-button name="Select All" icon=""></x-button>
                                        <x-button name="Select Objects" icon=""></x-button>
                                        <x-button name="Select With Similar Formatting" icon=""></x-button>
                                        <x-button name="Selection Pane..." icon=""></x-button>
                                    </template>
                                </x-menu-button>
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
import XMenuButton from "./components/XMenuButton.vue";
import XSplitButton from "./components/XSplitButton.vue";
import XSeparator from "./components/XSeparator.vue";
import XComboBox from "./components/XComboBox.vue";
import XRibbonTabInfo from "./models/XRibbonTabInfo";

@Component({
    components: {
        XRibbon,
        XRibbonGroup,
        XRibbonStack,
        XRibbonRow,
        XButton,
        XMenuButton,
        XSplitButton,
        XSeparator,
        XComboBox
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
    public fonts: string[] = [
        "Calibri",
        "Times New Roman"
    ];
    public currentFont = "Calibri";
    public fontSizes: string[] = [
        "6",
        "7",
        "8",
        "10",
        "11",
        "12",
        "14",
        "16",
        "20",
        "24",
        "28",
        "32",
        "36"
    ];
    public currentFontSize = "11";

    private potentialFonts = [
        "Lucida Console",
        "Monaco",
        "Courier New",
        "Courier",
        "Calibri",
        "Arial",
        "Helvetica",
        "Tahoma",
        "Geneva",
        "Georgia",
        "Palatino Linotype",
        "Book Antiqua",
        "Palatino",
        "Times New Roman",
        "Times"
    ];

    mounted() {
        this.fonts = this.potentialFonts;
    }

    onValidateFontSize(text: string) {
        return !isNaN(Number(text))
    }
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
    cursor: text;
}

.groups {
    display: flex;
}

.shift-left {
    margin-left: -1px;
}

#app {
    --app-accent: rgb(40, 110, 190);
    --app-ribbon: rgb(240, 240, 240);
    --app-content: rgb(225, 225, 225);
    --app-overlay: rgb(248, 248, 248);

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
