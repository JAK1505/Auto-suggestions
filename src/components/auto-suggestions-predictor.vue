<template>
  <div class="flex">
    <div>
      <vue-editor
        class="text-editor"
        ref="editor"
        v-model="textInput"
        placeholder="Type Here"
        @text-change="handleTextChange"
      />
    </div>
    <div
      v-if="suggestionsLoading || suggestions.length"
      class="suggestions-wrapper"
    >
      <span class="suggestions-title">Suggestions</span>
      <div
        v-if="suggestionsLoading"
        class="loading-wrapper"
      >
        <loading-dots />
      </div>
      <ul v-else-if="suggestions.length">
        <li
          v-for="(suggestion, idx) in suggestions"
          :key="idx"
          @click="suggestionSelected(suggestion)"
        >
          {{ suggestion }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import { debounce } from 'lodash';
import { VueEditor, Quill } from "vue2-editor/dist/vue2-editor.core.js";
import LoadingDots from './loading-dots.vue';

const Block = Quill.import('blots/block');
Block.tagName = 'DIV';
Quill.register(Block, true);

export default {
  name: "AutoSuggestionsPredictor",
  components: {
    VueEditor,
    LoadingDots,
  },
  data() {
    return {
      textInput: "",
      debounceFunction: () => {},
      suggestionsLoading: false,
      suggestions: [],
      isSuggestionSelected: false,
    };
  },
  computed: {
    editor() {
      return this.$refs.editor.quill;
    },
  },
  mounted() {
    this.focusEditor();
    this.debounceFunction = debounce(() => this.fetchSuggestions(), 750);
  },
  methods: {
    focusEditor() {
      this.editor.focus();
    },
    fetchSuggestions() {
      this.suggestionsLoading = true;
      setTimeout(() => {
        this.suggestionsLoading = false;
        this.suggestions = [
          'Amish',
          'Vaibhav',
          'Suneel',
          'Urvin',
        ];
      }, 2000);
    },
    suggestionSelected(suggestion) {
      this.isSuggestionSelected = true;
      const selection = this.editor.getSelection(true);
      this.editor.insertText(selection.index, suggestion);
    },
    handleTextChange() {
      if (this.isSuggestionSelected) {
        this.isSuggestionSelected = false;
        this.suggestions = [];
      } else {
        this.debounceFunction();
      }
    }
  },
};
</script>

<style scoped>
@import "~vue2-editor/dist/vue2-editor.css";
@import '~quill/dist/quill.core.css';
@import '~quill/dist/quill.bubble.css';
@import '~quill/dist/quill.snow.css';

  .flex {
    display: flex;
  }

  .text-editor {
    height: 40vh;
    width: 75vw;
  }

  .suggestions-wrapper {
    width: 100%;
    height: 40vh;
    overflow: auto;
    margin: 0 8px;
    padding: 16px;
    border: 1px solid #d3d8e3;
    border-radius: 8px;
    background-color: #E3F99D;
  }

  .suggestions-wrapper li {
    cursor: pointer;
  }

  .suggestions-title {
    font-size: 28px;
    font-weight: 700;
  }

  .loading-wrapper {
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
  }
</style>