<template>
  <div class="editor-container">
    <h1>Rich Text</h1>
    <div class="options">
      <button v-on:click="editText('Bold', null)" class="button" id="bold-button" title="Bold">B</button>
      <button
        v-on:click="editText('Italic', null)"
        class="button"
        id="italic-button"
        title="Italic"
      >
        <em>I</em>
      </button>

      <button
        v-on:click="editText('Superscript', null)"
        class="button"
        id="sup-button"
        title="Superscript"
      >
        X
        <sup>2</sup>
      </button>
      <button
        v-on:click="editText('Subscript', null)"
        class="button"
        id="sub-button"
        title="Subscript"
      >
        X
        <sub>2</sub>
      </button>

      <button
        v-on:click="editText('Strikethrough', null)"
        class="button"
        id="strike-button"
        title="Strikethrough"
      >
        <s>abc</s>
      </button>

      <button
        v-on:click="createList('InsertOrderedList')"
        class="button"
        id="ordered-list-button"
        title="Numbered list"
      >(i)</button>
      <button
        v-on:click="createList('InsertUnorderedList')"
        class="button"
        id="unordered-list-button"
        title="Bulleted list"
      >&bull;</button>

      <input
        v-on:change="editText('ForeColor', $event.target.value)"
        class="button-color"
        type="color"
        id="font-color-button"
        title="Change Font Color"
      />
      <input
        v-on:change="editText('BackColor', $event.target.value)"
        class="button-color"
        type="color"
        id="highlight-button"
        title="Highlight Text"
      />

      <select
        v-on:change="editText('FontName', $event.target.value)"
        name="font-changer"
        id="font-changer"
        title="Change Font"
      >
        <option value="Times New Roman">Times New Roman</option>
        <option value="Consolas">Consolas</option>
        <option value="Tahoma">Tahoma</option>
        <option value="monospace">Monospace</option>
        <option value="cursive">Cursive</option>
        <option value="sans-serif">Sans-Serif</option>
        <option value="Calibri">Calibri</option>
      </select>

      <select
        v-on:change="editText('FontSize', $event.target.value)"
        name="font-size-changer"
        id="font-size-changer"
        title="Change Font Size"
      >
        <option key="1" value="1">1</option>
        <option key="2" value="2">2</option>
        <option key="3" value="3">3</option>
        <option key="4" value="4">4</option>
        <option key="5" value="5">5</option>
        <option key="6" value="6">6</option>
        <option key="7" value="7">7</option>
        <option key="8" value="8">8</option>
      </select>

      <button
        v-on:click="editText('CreateLink', null, true)"
        class="button"
        id="link-button"
        title="Create Link"
      >Link</button>
      <button
        v-on:click="editText('UnLink', null)"
        class="button"
        id="un-link-button"
        title="Unlink"
      >Unlink</button>
      <button
        v-on:click="editText('undo', null)"
        class="button"
        id="undo-button"
        title="Undo the previous action"
      >&larr;</button>
      <button
        v-on:click="editText('redo', null)"
        class="button"
        id="redo-button"
        title="Redo"
      >&rarr;</button>
    </div>
    <div class="richtext">
      <iframe title="richtext" name="richtext" id="richtext" frameborder="0"></iframe>
    </div>
  </div>
</template>

<script>
const editor = document.getElementsByName("richtext");
var doc;

export default {
  name: "Editor",
  mounted() {
    window.addEventListener("load", () => {
      let frame = editor[0].contentDocument || editor[0].contentWindow.document;
      frame.designMode = "on";
      doc = frame;
    });
  },
  methods: {
    editText: function(action, comp, isLink = false) {
      if (isLink) {
        let url = prompt("Enter with a URL", "http://");
        comp = url;
      }
      doc.execCommand(action, false, comp);
    },
    createList: function(action) {
      let comp = "newOL" + Math.round(Math.random() * 1000);
      this.editText(action, comp);
    }
  }
};
</script>

<style scoped>
.editor-container {
  margin: 30px auto;
  width: 650px;
  height: 200px;
  background: #f0f0f5;
}

.editor-container h1 {
  font-size: 30px;
  text-align: center;
}

.editor-container .options {
  border-bottom: none;
  padding: 10px;
  background-color: #451846;
  color: #fff;
  border-radius: 8px 8px 0px 0px;
  width: 746px;
  margin-top: 10px;
}

.editor-container .options .button {
  color: #fff;
  border: none;
  outline: none;
  background-color: transparent;
  cursor: pointer;
  margin: 0 5px;
}

.editor-container .options .button:hover {
  color: #c5afc7;
  transition: all 0.3s linear 0s;
}

.editor-container .options .button-color {
  border: none;
  outline: none;
  background-color: transparent;
  margin: 0 5px;
  cursor: pointer;
}

.editor-container .options select {
  color: #333;
  border: 1px solid #dcdce6;
  border-radius: 2px;
  padding: 0 10px;
  margin: 0 5px;
  cursor: pointer;
}

.editor-container .richtext {
  border: 2px solid rgb(16, 17, 17);
  height: 100%;
  width: 746px;
  background-color: #fff;
  align-items: center;
}

iframe#richtext {
  height: 100%;
  width: 100%;
}
</style>
